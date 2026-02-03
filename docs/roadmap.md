# Roadmap

This roadmap outlines the future direction for JustSearch. Features listed here are planned for **6-12+ months** out — timelines are subject to change based on user feedback and development priorities.

## Current Focus

The current development focus is on:
- **Stability**: Ensuring reliable operation across diverse Windows environments
- **Search quality**: Improving ranking, relevance, and result presentation
- **Onboarding**: Streamlining installation and first-run experience
- **Performance**: Optimizing indexing speed and memory usage

## Planned Features

### Cloud Connectors Framework

**Goal**: Expand searchable content beyond local files without compromising the local-first promise.

**How it works**:
- Connectors pull data from cloud services (Google Drive, Slack, GitHub, etc.)
- Data is normalized and stored locally in a managed directory
- Existing indexer processes the local copies — search stays fast and private
- You control sync frequency and which folders/channels to include

**Why it matters**:
- A search tool with 10% of your data is 10% useful; one with 100% is indispensable
- Users live across multiple services — local-only is limiting
- Maintains privacy: data pulled to your machine, never pushed to our servers

**Tentative scope**:
- Google Drive (documents, spreadsheets)
- GitHub (repositories, issues, wikis)
- Slack (messages, files)
- Notion (pages, databases)

---

### Audio Intelligence ("Meeting Brain")

**Goal**: Index spoken content from meetings, voice notes, and recordings.

**How it works**:
- Drop audio/video files (MP3, M4A, MP4, etc.) or point to recording folders
- Transcription via Whisper (local, runs on GPU or CPU)
- Transcripts indexed with timestamps
- Search hits link directly to the relevant moment in the recording

**Why it matters**:
- "What did we agree on in that meeting?" is a universal pain point
- Meetings generate hours of content but no searchable artifacts
- Integrates with existing "search → inspect → answer" workflow

**Tentative scope**:
- Local audio file transcription
- Zoom local recordings support
- Timestamp-linked search results
- Speaker diarization (if feasible locally)

---

### Active File Management (Agentic Operations)

**Goal**: Let the AI help organize your files, not just read them.

**How it works**:
- New command mode actions: `/organize`, `/rename`, `/dedupe`
- Example: "Organize my Downloads folder by project"
- AI proposes a plan with preview (UI shows diff of proposed changes)
- User reviews and approves before any files are moved

**Why it matters**:
- Moves from "passive observer" to "active assistant"
- File organization is tedious but important
- Human-in-the-loop ensures safety

**Tentative scope**:
- Folder organization by topic/project
- Duplicate detection and cleanup suggestions
- Bulk rename with pattern recognition
- Archive suggestions for old files

---

### Contextual Feeds (Smart Launchpad)

**Goal**: Proactively surface relevant information instead of waiting for searches.

**How it works**:
- Home screen shows "What changed while you were away?"
- Auto-summarizes changes in starred/watched folders
- Aggregates activity across connectors into daily digests
- "Project X Update": commits + new docs + relevant messages in one view

**Why it matters**:
- Increases engagement — open the app to "check in", not just when you've lost something
- Reduces context-switching between multiple apps
- Personalized without cloud profiling

**Tentative scope**:
- Folder change summaries
- Cross-source project aggregation
- Customizable digest frequency
- Priority/importance signals

---

## Not Planned (Currently)

To maintain focus, some features are explicitly **not** on the roadmap:

- **Mobile apps**: Focus remains on desktop (Windows first, then macOS/Linux)
- **Real-time collaboration**: JustSearch is a personal tool, not a team workspace
- **Cloud hosting**: Core product remains local-first; cloud features would be optional add-ons
- **Browser extension**: May reconsider after core product stabilizes

---

## Feedback

Have ideas for features? Want to influence priorities?

- Open an issue on [GitHub](https://github.com/eliasjustus/justsearch-releases/issues)
- Describe the problem you're trying to solve (not just the feature you want)

The roadmap evolves based on real user needs.
