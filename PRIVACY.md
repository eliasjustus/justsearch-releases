# Privacy Policy

JustSearch is designed with privacy as a core principle. This document explains what data is collected, stored, and processed.

## Summary

- **Your files stay on your machine** — JustSearch indexes and searches locally
- **No cloud uploads** — Core features work without internet
- **No cloud telemetry** — Usage metrics are stored locally only
- **You control AI setup** — Model downloads are user-initiated

---

## Data That Stays Local

### Your Files and Index
- Files you add to the index are processed entirely on your machine
- The search index (Lucene) is stored in your local app data folder
- No file content is ever uploaded to external servers

### Search Queries
- Search queries are processed locally
- Queries are **redacted** from logs (marked as `[REDACTED]`) to protect privacy
- No search history is sent anywhere

### AI Models
- AI models are downloaded **only when you initiate** the "Install AI" flow
- Downloads are from pinned, hash-verified sources (Hugging Face)
- Models are stored locally in your app data folder
- All AI inference runs on your machine

---

## Local Telemetry (What We Log)

JustSearch writes local diagnostic logs and metrics for debugging. These are stored in:

```
%APPDATA%\io.justsearch.shell\logs\
%APPDATA%\io.justsearch.shell\telemetry\
```

### What's Logged
- **Performance metrics**: API response times, indexing throughput (no query content)
- **Error logs**: Stack traces for debugging crashes
- **System info**: JVM memory usage, thread counts

### What's NOT Logged
- File contents
- Search queries (redacted)
- Personal information
- Usage patterns sent to any server

### Log Format
Metrics use NDJSON (Newline Delimited JSON) format for easy inspection:
```json
{"t":"2026-01-02T10:00:01Z","name":"api.request_ms","type":"histogram","p50":200,"tags":{"route":"/api/knowledge/search"}}
```

---

## Network Access

### When JustSearch Uses the Network

| Feature | Network Use | User Control |
|---------|-------------|--------------|
| Core search | None | Always local |
| "Install AI" | Downloads models from Hugging Face | User-initiated only |
| Offline AI Packs | None (import from local files) | Fully offline option |

### Loopback-Only API
The local API server binds to `127.0.0.1` only — it cannot be accessed from other machines on your network.

---

## Third-Party Services

### Model Downloads
When you use "Install AI", models are downloaded from:
- **Hugging Face** (huggingface.co) — Model hosting platform

Downloads are:
- Hash-verified (SHA-256) before use
- Stored permanently in your local app data
- Not re-downloaded unless you request it

### No Analytics or Tracking
JustSearch does not include:
- Google Analytics or similar
- Crash reporting services (e.g., Sentry)
- Usage tracking SDKs
- Advertising frameworks

---

## Data Deletion

To remove all JustSearch data:

1. Uninstall JustSearch via Windows Settings
2. Delete the app data folder:
   ```
   %APPDATA%\io.justsearch.shell\
   ```

This removes:
- Search index
- Downloaded AI models
- Logs and metrics
- All settings

---

## Questions?

If you have privacy questions or concerns:
- Email: eliasjustus457@gmail.com
- GitHub: [justsearch-releases/issues](https://github.com/eliasjustus/justsearch-releases/issues)
