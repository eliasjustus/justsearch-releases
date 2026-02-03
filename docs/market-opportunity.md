# Market Opportunity

## Executive Summary

JustSearch targets the intersection of two growing markets: **AI-powered productivity tools** and **privacy-first software**. As AI capabilities expand and privacy regulations tighten, there's increasing demand for tools that deliver AI benefits without requiring data to leave the user's machine.

## The Problem Space

### Information Overload
Knowledge workers spend **2+ hours per day** searching for information across fragmented tools and file systems. Documents accumulate across folders, cloud services, and applications with no unified way to find or interrogate them.

### The Cloud Trust Problem
Modern AI assistants (ChatGPT, Copilot, Notion AI) require uploading data to external servers. For many users and organizations, this creates unacceptable risks:
- **Regulatory compliance**: GDPR, HIPAA, SOC 2, and industry-specific regulations restrict data handling
- **Intellectual property**: Proprietary code, research, and business documents can't be uploaded
- **Personal privacy**: Users increasingly uncomfortable with data collection

### The Local AI Gap
Until recently, running capable AI locally was impractical. Hardware requirements were prohibitive, models were too large, and tooling was immature. This is changing rapidly:
- Consumer GPUs now handle 7B-13B parameter models comfortably
- Quantization techniques (GGUF) dramatically reduce memory requirements
- "AI PC" marketing is normalizing local AI expectations

## Market Sizing

### Total Addressable Market (TAM)

**Global knowledge worker productivity software**: ~$50B annually, growing 10-15% YoY

**Windows PC installed base**: 1.4B+ monthly active devices (Microsoft, 2024)

### Serviceable Addressable Market (SAM)

**GPU-capable Windows PCs** (proxy from gaming/creator segment):
- ~25-30% of Windows PCs have discrete GPUs
- ~70% of discrete GPUs are NVIDIA (best llama.cpp support)
- Estimated **250-300M** devices capable of GPU-accelerated local AI

**Tier breakdown by VRAM** (Steam Hardware Survey as proxy):
- 12GB+ VRAM (best experience): ~30% of GPU users → **75-100M devices**
- 8GB+ VRAM (good experience): ~65% of GPU users → **160-200M devices**

### Serviceable Obtainable Market (SOM)

Initial beachhead: **Developers and technical knowledge workers** who:
- Work with codebases + documentation
- Handle sensitive/proprietary information
- Have capable hardware (often for development/gaming)
- Value privacy and control

Conservative SOM estimate: **1-5% of SAM** over multi-year horizon for niche prosumer tool = **2-10M potential users**

## Competitive Landscape

### Windows Copilot (Microsoft)
- **Strengths**: Pre-installed, massive distribution, Microsoft integration
- **Weaknesses**: Cloud-dependent, limited file indexing, generic assistant
- **Our wedge**: Depth, trust (citations), offline capability, whole-corpus indexing

### Khoj / Local-first "Second Brain" Tools
- **Strengths**: Open source, extensible, cross-platform
- **Weaknesses**: Setup complexity, broad but shallow, developer-focused UI
- **Our wedge**: Narrower focus, polished Windows experience, faster time-to-value

### Cursor / Sourcegraph Cody (Code Intelligence)
- **Strengths**: Deep IDE integration, code-specific features, developer mindshare
- **Weaknesses**: Code-only, cloud models, subscription pricing
- **Our wedge**: Mixed corpus (code + docs + PDFs), local-first, citations

### Perplexity / Web AI Assistants
- **Strengths**: Real-time web access, strong models, clean UX
- **Weaknesses**: Cloud-only, no local file access, subscription for heavy use
- **Our wedge**: Local files are the corpus, privacy, offline capability

## Positioning

> **JustSearch** is a Windows-first, local-first app that lets you **search and ask questions across your files** and get **answers grounded in cited sources** you can verify instantly.

### Core Promise
1. **Completeness**: Answers based on your chosen corpus, not a "recent files" subset
2. **Trust**: Citations and instant verification (open → highlight → iterate)
3. **Responsiveness**: Fast enough to become habitual
4. **Local-first**: Core workflows don't require uploading sensitive content

### Messaging Pillars
1. **"Answer with citations"** — Get answers you can verify
2. **"Local-first privacy"** — Your files stay on your machine
3. **"Fast search + inspect"** — Find the exact passage in seconds
4. **"Built for builders"** — Works for codebases and docs, not just filenames

## Business Model (Planned)

### Free Local Tier
- Full local search and AI features
- No account required
- Unlimited local files

### Paid Online Features (Future)
- Cloud connectors (Google Drive, Slack, GitHub sync)
- Cross-device sync
- Priority support

### Enterprise (Later)
- Policy management and allowlists
- Offline deployment packs
- Volume licensing

## Why Now?

1. **Hardware inflection**: Consumer GPUs increasingly capable of useful local AI
2. **Model quality**: Open-weight models (Llama, Mistral, Phi) now competitive for many tasks
3. **Privacy awareness**: Post-ChatGPT, users understand AI value but worry about data
4. **Regulatory pressure**: GDPR, CCPA, industry compliance making cloud uploads problematic
5. **"AI PC" narrative**: Microsoft/Intel/AMD normalizing local AI expectations

## Risks and Mitigations

| Risk | Mitigation |
|------|------------|
| Microsoft bundles better local AI into Windows | Focus on power-user features, citation UX, multi-source corpus |
| Local models plateau in quality | Hybrid approach: local for privacy-sensitive, optional cloud for complex queries |
| Hardware requirements limit adoption | CPU fallback, tiered feature set, optimize for 8GB VRAM |
| Open source alternatives commoditize features | UX polish, reliability, "just works" value proposition |

## Summary

JustSearch addresses a real pain point (finding information in personal files) with a differentiated approach (local AI with citations) at a moment when the enabling technology (consumer GPUs, open-weight models) has matured sufficiently.

The beachhead is clear (developers and technical knowledge workers), the competition has gaps (cloud-only or too complex), and the market trend (privacy + local AI) supports the thesis.
