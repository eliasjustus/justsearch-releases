# Changelog

All notable changes to JustSearch will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0-alpha] - 2026-02-03

### Added
- Local file indexing with support for documents, PDFs, code files, and images (via OCR)
- Semantic search powered by local LLMs
- Q&A functionality with cited sources — click citations to jump to source passages
- Three-process architecture (Head/Body/Brain) for crash isolation and stability
- Graceful degradation — works without GPU, falls back to keyword search
- Real-time file watching for incremental index updates
- Windows installer (NSIS)

### Known Limitations
- Windows only (macOS/Linux not yet available)
- First indexing run may be slow on large file sets
- Some complex PDF layouts may not extract perfectly
- AI features require compatible NVIDIA GPU for best performance

[0.1.0-alpha]: https://github.com/eliasjustus/justsearch-releases/releases/tag/v0.1.0-alpha
