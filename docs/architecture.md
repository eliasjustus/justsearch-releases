# Architecture

JustSearch uses a **Local-First Microservices** architecture — it runs entirely on your machine but mimics the resilience patterns of distributed cloud systems.

## Why This Design?

Desktop applications face unique challenges:
- **File locking on Windows**: Two processes accessing the same file can cause corruption
- **UI responsiveness**: Users expect the interface to stay responsive even during heavy operations
- **Resource contention**: Indexing, searching, and AI inference all compete for CPU/GPU/memory

Cloud systems solve these with separate services. We bring the same pattern to desktop.

## The Three-Process Model

```
┌─────────────────────────────────────────────────────────────────────┐
│                         JustSearch                                   │
│                                                                      │
│  ┌────────────────────┐                                             │
│  │       HEAD         │  UI Host + API Gateway                      │
│  │  (Main Process)    │  • Runs the React UI                        │
│  │                    │  • Exposes REST API for frontend            │
│  │  modules/ui        │  • Orchestrates other processes             │
│  │  modules/ui-web    │  • NEVER touches Lucene files               │
│  │  modules/shell     │                                             │
│  └─────────┬──────────┘                                             │
│            │ gRPC + Memory-Mapped Files                             │
│            ▼                                                        │
│  ┌────────────────────┐                                             │
│  │       BODY         │  Knowledge Server                           │
│  │  (Worker Process)  │  • Owns Lucene index exclusively            │
│  │                    │  • Extracts text via Apache Tika            │
│  │  indexer-worker    │  • Handles search queries                   │
│  │                    │  • Auto-restarts on crash (up to 3x)        │
│  └────────────────────┘                                             │
│                                                                      │
│  ┌────────────────────┐                                             │
│  │       BRAIN        │  Inference Server                           │
│  │  (Native Binary)   │  • Runs llama.cpp for local LLM             │
│  │                    │  • Manages VRAM allocation                  │
│  │  llama-server.exe  │  • Handles embeddings + generation          │
│  │                    │  • Health-monitored, auto-recovers          │
│  └────────────────────┘                                             │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## Design Principles

### "One Owner" Policy
Every piece of data has exactly one process that can write to it:
- **Lucene Index**: Owned exclusively by Body (Knowledge Server)
- **Configuration**: Owned by Head, passed to children at startup
- **VRAM**: Owned by Brain (one model loaded at a time)

This eliminates file locking issues that plague monolithic desktop apps on Windows.

### "Verify, Don't Guess"
The system uses deterministic state checking instead of assumptions:
- **Port discovery**: Processes bind to ephemeral ports and communicate actual ports via memory-mapped files
- **Health checks**: Frontend polls `/api/status` to know backend state, not timers
- **Lifecycle gates**: Automation uses `/api/health` as a contract-tested readiness gate

### Graceful Degradation
The system works even when parts fail:
- **No GPU?** Inference Manager detects VRAM shortage, disables AI features, falls back to keyword search
- **Worker crash?** UI stays responsive, shows "Index Offline" state, watchdog restarts worker
- **Model too large?** Automatically uses smaller context window or refuses to load (no silent OOM)

## Inter-Process Communication

### Head ↔ Body: gRPC + Memory-Mapped Files
- **gRPC**: Structured data transfer (search requests, index operations)
- **MMF**: Sub-millisecond signaling and port discovery

### Head ↔ Brain: HTTP
- Standard HTTP API to llama-server
- Health polling for crash detection
- Props endpoint for capability discovery

## Key Technologies

| Component | Technology | Why |
|-----------|------------|-----|
| Search engine | Apache Lucene | Battle-tested, HNSW vector support, no external server needed |
| Content extraction | Apache Tika | Handles 1000+ file formats (PDF, Office, images via OCR) |
| Local LLM | llama.cpp | Fast CPU/GPU inference, GGUF model format, active community |
| UI | React + Tauri | Modern web UI in native desktop shell |
| Backend | Java 21+ | Strong typing, mature ecosystem, Panama FFM for native interop |

## Why Not Simpler?

A single-process app would be simpler to build but:
1. **Lucene file locking** on Windows is brutal — one process touching index files while another reads causes `LockObtainFailedException`
2. **UI freezes** during heavy operations are unacceptable for a search tool
3. **Crash propagation** means a poison PDF (via Tika) would crash your entire app

The three-process model adds complexity but delivers the reliability users expect.
