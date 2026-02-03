# Product Overview

JustSearch is a **local-first neural search engine** that lets you search and ask questions across your personal files using AI — without uploading anything to the cloud.

## What It Does

1. **Indexes your files** — Documents, PDFs, code, images (via OCR). Watches for changes and updates automatically.

2. **Semantic search** — Find files by meaning, not just keywords. "Budget meeting notes from last quarter" finds relevant documents even without exact keyword matches.

3. **AI-powered Q&A** — Ask questions about your files in natural language. Get answers with clickable citations to verify sources instantly.

4. **100% local processing** — All indexing and AI inference runs on your machine. No cloud uploads, no API keys required for core features.

## How It Works

JustSearch runs as three coordinated processes on your machine:

```
┌─────────────────────────────────────────────────────────────┐
│                     Your Computer                            │
│                                                              │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────┐     │
│  │    HEAD      │   │    BODY      │   │    BRAIN     │     │
│  │  (UI + API)  │──▶│  (Indexing)  │──▶│    (AI)      │     │
│  │              │   │              │   │              │     │
│  │ React + Java │   │ Lucene+Tika  │   │ llama.cpp    │     │
│  └──────────────┘   └──────────────┘   └──────────────┘     │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │                   Your Files                          │   │
│  │  Documents • PDFs • Code • Images • Notes             │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

This architecture ensures:
- **Isolation**: A crash in one component doesn't bring down the others
- **Responsiveness**: Heavy indexing doesn't freeze your UI
- **Graceful degradation**: No GPU? Works with keyword search. GPU available? Enables AI features.

## Key Differentiators

### vs. Windows Search / Everything
- Semantic understanding (not just filename/keyword matching)
- AI Q&A with cited sources
- Works across file types (PDFs, images via OCR)

### vs. Cloud AI Assistants (Copilot, ChatGPT)
- Your data never leaves your machine
- No subscription required for core features
- Works offline
- Indexes YOUR files, not just recent ones

### vs. Other Local Search Tools (Khoj, etc.)
- Purpose-built "search → inspect → answer" loop
- Windows-first with proper file locking handling
- Lower setup friction (bundled models, no configuration)

## Target Users

**Developers**: Search codebases + documentation together. Find that function you wrote six months ago by describing what it does.

**Researchers**: Manage literature, notes, and drafts. Ask questions across your corpus and get cited answers.

**Knowledge Workers**: Search contracts, reports, presentations. Never lose a document again.

**Privacy-Conscious Professionals**: Legal, healthcare, finance — industries where uploading to cloud isn't an option.

## Current Status

JustSearch is in active development. Core search and AI Q&A functionality works. Focus areas:
- Stability and performance optimization
- Search quality improvements
- Installer and onboarding polish

First public release coming soon.
