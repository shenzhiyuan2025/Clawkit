
<h1 align="center">ClawKit</h1>

<p align="center">
  <strong>Agent's Widget-in-Chat Protocol & Open Ecosystem</strong><br/>
  Let every Agent speak GUI.
</p>
<img width="270" height="276" alt="image" src="https://github.com/user-attachments/assets/c9a569da-89df-4b77-8920-55ada936d6b9" align="center"/>
<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="docs/PROTOCOL.md">Protocol Spec</a> ·
  <a href="docs/ARCHITECTURE.md">Architecture</a> ·
  <a href="docs/WIDGET_CATALOG.md">Widget Catalog</a> ·
  <a href="docs/CONTRIBUTING.md">Contributing</a> ·
  <a href="#demo">Live Demo</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
  <img src="https://img.shields.io/badge/protocol-v0.1-purple.svg" alt="Protocol Version" />
  <img src="https://img.shields.io/badge/widgets-30+-green.svg" alt="Widget Count" />
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome" />
</p>

---

## What is ClawKit?

**ClawKit is an open-source Widget-in-Chat protocol and ecosystem that lets any AI conversation product embed interactive GUI components directly in the dialogue flow.**

Today, 99% of AI agents communicate through pure text. But text is a bottleneck — showing 10 restaurants on a map takes 3 seconds with GUI, 30 seconds with text. ClawKit bridges this gap by providing:

- 🔌 **A dead-simple protocol** — add a `widgets` field to your agent's JSON response
- 📦 **30+ built-in widgets** — maps, charts, forms, product cards, timelines, and more
- 🌍 **An open Widget Registry** — anyone publishes widgets, any agent uses them
- 🧠 **A recommendation engine** — context-aware widget suggestions that get smarter over time
- 🎨 **Multi-framework renderers** — React, Vue, Flutter, Mini Programs

```
┌──────────────────────────────────────────────────┐
│  Your Chat App (any conversation product)        │
│  ┌────────────────────────────────────────────┐  │
│  │  ClawKit Renderer (React/Vue/Flutter/...)  │  │
│  │  Auto-renders widgets in dialogue flow     │  │
│  └──────────────────┬─────────────────────────┘  │
└─────────────────────┼────────────────────────────┘
                      │  ClawKit Protocol (JSON)
┌─────────────────────┼────────────────────────────┐
│  Agent Backend (any AI agent)                    │
│  + ClawKit SDK (Python / TypeScript / Java)      │
└──────────────────┬──────────────┬────────────────┘
                   ↓              ↓
        ┌──────────────┐  ┌─────────────────┐
        │ Widget       │  │ Recommend API   │
        │ Registry     │  │ (context-aware  │
        │ (open market)│  │  suggestions)   │
        └──────────────┘  └─────────────────┘
```
<img width="2840" height="6910" alt="image" src="https://github.com/user-attachments/assets/4b754ed7-4c44-4e89-aa21-071d68a32edf" />

## Why ClawKit?

| Problem | Current State | ClawKit Solution |
|---------|--------------|-----------------|
| Agents can only output text | Pure text dialogue is low-bandwidth | Rich GUI widgets embedded in chat |
| Adding GUI to agents is hard | Requires frontend expertise | **3 lines of code** on agent side |
| No reusable widget ecosystem | Everyone reinvents the wheel | **Open Registry** with 30+ built-in widgets |
| Existing protocols are complex | A2UI requires custom Renderer + Catalog | **Plug and play** — one component wraps your chat |

### How ClawKit compares

| | ClawKit | A2UI (Google) | MCP Apps | CopilotKit |
|---|---------|--------------|----------|------------|
| **What it is** | Widget ecosystem + protocol | Protocol spec only | Platform-embedded apps | Agent frontend framework |
| **Widget source** | Open Registry (community) | Self-built catalog | Developer-written web apps | Self-built components |
| **Agent-side effort** | 3 lines of JSON | Implement full Renderer | Build MCP Server + Web UI | Learn framework API |
| **Cross-app embedding** | ✅ Any chat product | Needs custom Renderer | ChatGPT/Claude only | Framework-dependent |
| **Data flywheel** | ✅ Recommendation engine | ❌ | ❌ | ❌ |
| **Built-in widgets** | 30+ production-ready | 18 basic primitives | None | None |

---

## Demo
![Uploading image.png…]()



**Ten scenario demos included:**

| Scenario | Widgets Used | Description |
|----------|-------------|-------------|


> 🚀 **Try the live demo**: `npx create-ClawKit-app my-demo && cd my-demo && npm run dev`

---

## Quick Start

### For Agent Developers (Backend)

Add widgets to your agent's response — that's it:

```python
# pip install ClawKit

from ClawKit import ClawKitResponse

response = ClawKitResponse(
    text="Here are nearby restaurants:",
    widgets=[
        {
            "type": "ClawKit/map-list",
            "data": {
                "locations": [
                    {"name": "Sushi Zen", "lat": 31.23, "lng": 121.47, "rating": 4.8},
                    {"name": "Pasta House", "lat": 31.22, "lng": 121.48, "rating": 4.6},
                ],
                "center": {"lat": 31.23, "lng": 121.47}
            }
        }
    ]
)
```

### For Frontend Developers (Client)

Wrap your existing chat with one component:

```tsx
// npm install @ClawKit/react

import { ClawKitChat } from '@ClawKit/react'

function App() {
  return (
    <ClawKitChat
      messages={messages}
      onAction={(action) => handleAction(action)}
    />
  )
}
```

### For Widget Developers (Ecosystem)

Publish your component to the ClawKit Registry:

```tsx
// Register any React component as a ClawKit widget
import { registerWidget } from '@ClawKit/registry'

registerWidget({
  type: "mycompany/stock-chart",
  component: StockChartComponent,
  schema: stockChartSchema,       // JSON Schema for data validation
  promptHint: "Display a stock price chart with candlestick view",
})
```

---

## Widget Catalog (v0.1)

ClawKit ships with **30+ production-ready widgets** across 6 categories:

### 📊 Data Display
| Widget | Type ID | Description |
|--------|---------|-------------|
| Metric Card | `ClawKit/metrics` | KPI cards with trend indicators |
| Chart | `ClawKit/chart` | Line, bar, pie, area charts |
| DataTable | `ClawKit/data-table` | Sortable, filterable data table |
| Progress Ring | `ClawKit/progress` | Circular progress indicator |
| Timeline | `ClawKit/timeline` | Step-by-step event timeline |
| Comparison | `ClawKit/comparison` | Side-by-side feature comparison |

### 📝 Form & Input
| Widget | Type ID | Description |
|--------|---------|-------------|
| Smart Form | `ClawKit/form` | Dynamic form with validation |
| Stepper | `ClawKit/stepper` | Multi-step wizard |
| Date Picker | `ClawKit/date-picker` | Date/time selection |
| File Picker | `ClawKit/file-picker` | File upload with preview |
| Rating | `ClawKit/rating` | Star/emoji rating input |
| Choice Chips | `ClawKit/choice-chips` | Single/multi select chips |

### 🗺️ Location & Map
| Widget | Type ID | Description |
|--------|---------|-------------|
| Map | `ClawKit/map` | Interactive map view |
| Map List | `ClawKit/map-list` | Map + location list combo |
| Route View | `ClawKit/map-route` | Origin → destination with route |
| Location Picker | `ClawKit/location-picker` | Select a location on map |

### 🛍️ Product & Media
| Widget | Type ID | Description |
|--------|---------|-------------|
| Product Card | `ClawKit/product-card` | Product with image, price, rating |
| Product Carousel | `ClawKit/product-carousel` | Swipeable product cards |
| Gallery | `ClawKit/gallery` | Image gallery with lightbox |
| Video Player | `ClawKit/video` | Embedded video player |
| Audio Player | `ClawKit/audio` | Audio player with waveform |

### 🔄 Flow & Action
| Widget | Type ID | Description |
|--------|---------|-------------|
| Action Buttons | `ClawKit/actions` | Contextual action buttons |
| Quick Actions | `ClawKit/quick-actions` | Pill-shaped quick reply buttons |
| Checklist | `ClawKit/checklist` | Interactive todo checklist |
| Confirm Dialog | `ClawKit/confirm` | Confirmation with options |
| Status Badge | `ClawKit/status` | Status indicator |

### 💬 Emotion & Feedback
| Widget | Type ID | Description |
|--------|---------|-------------|
| Emotion Feedback | `ClawKit/emotion` | Empathetic response with avatar |
| Context Icon | `ClawKit/context-icon` | Contextual icon/illustration |
| Loading Narrative | `ClawKit/loading` | Story-driven loading state |
| Feedback Prompt | `ClawKit/feedback` | Thumbs up/down + comment |

> **See full catalog**: [docs/WIDGET_CATALOG.md](docs/WIDGET_CATALOG.md)
>
> **All built-in widgets use the same API as third-party widgets.** No special privileges. You can override, extend, or replace any official widget.

---

## Protocol Overview

ClawKit Protocol is intentionally minimal. A widget embedding requires only 3 fields:

```json
{
  "type": "ClawKit/map-route",
  "data": { "origin": {...}, "destination": {...} },
  "options": { "style": "compact" }
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `type` | ✅ | Widget identifier from Registry (`namespace/name`) |
| `data` | ✅ | Widget-specific data payload (validated against JSON Schema) |
| `options` | ❌ | Display options (style, size, theme, locale) |
| `actions` | ❌ | Callback definitions for user interactions |
| `fallback` | ❌ | Plain text fallback if widget unavailable |

### Message Format

ClawKit does **not** replace your existing message format. It adds an optional `widgets` array:

```json
{
  "role": "assistant",
  "content": "I found these restaurants for you:",
  "widgets": [
    { "type": "ClawKit/map-list", "data": {...} },
    { "type": "ClawKit/quick-actions", "data": {...} }
  ]
}
```

### Trust Levels

Widgets operate at two trust levels:

| Level | Mechanism | Security | Expressiveness |
|-------|-----------|----------|---------------|
| **L1 Declarative** | Pure JSON schema + data binding | Highest (no code execution) | Medium |
| **L2 Interactive** | Sandboxed JS with Registry review | High (sandbox + audit) | High (drag, animation, complex logic) |

### Interaction Model

```
User clicks button in widget
        ↓
ClawKit Renderer captures action event
        ↓
Event dispatched to Agent backend
{
  "action": "call_ride",
  "widgetType": "ClawKit/map-route",
  "context": { "origin": {...}, "destination": {...} }
}
        ↓
Agent processes and responds (possibly with new widgets)
```

> **Full protocol specification**: [docs/PROTOCOL.md](docs/PROTOCOL.md)

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                              │
│                                                              │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────────┐  │
│  │  React   │ │   Vue    │ │ Flutter  │ │ Mini Program  │  │
│  │ Renderer │ │ Renderer │ │ Renderer │ │   Renderer    │  │
│  └─────┬────┘ └─────┬────┘ └─────┬────┘ └──────┬────────┘  │
│        └────────────┬────────────┴──────────────┘            │
│                     │                                        │
│           ┌─────────┴─────────┐                              │
│           │  @ClawKit/core    │  Protocol parser, validator, │
│           │                   │  widget resolver, action bus │
│           └─────────┬─────────┘                              │
└─────────────────────┼────────────────────────────────────────┘
                      │  HTTP / WebSocket / SSE / AG-UI
┌─────────────────────┼────────────────────────────────────────┐
│                 SERVER LAYER                                  │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │ Agent SDK    │  │ Widget       │  │ Recommend API    │   │
│  │ Python/TS/   │  │ Registry     │  │                  │   │
│  │ Java         │  │              │  │ Context → Widget │   │
│  │              │  │ Search,      │  │ suggestions      │   │
│  │ Helpers for  │  │ Publish,     │  │                  │   │
│  │ building     │  │ Validate,    │  │ Learns from      │   │
│  │ widget JSON  │  │ Version      │  │ usage data       │   │
│  └──────────────┘  └──────────────┘  └──────────────────┘   │
└──────────────────────────────────────────────────────────────┘
```

### Core Packages

| Package | Description | Status |
|---------|-------------|--------|
| `@ClawKit/protocol` | JSON Schema definitions, TypeScript types, validators | 🚧 In Development |
| `@ClawKit/core` | Protocol parser, widget resolver, action event bus | 🚧 In Development |
| `@ClawKit/react` | React Renderer — `<ClawKitChat>` component | 🚧 In Development |
| `@ClawKit/vue` | Vue 3 Renderer | 📋 Planned |
| `@ClawKit/flutter` | Flutter Renderer | 📋 Planned |
| `ClawKit` (Python) | Python SDK for agent developers | 🚧 In Development |
| `@ClawKit/sdk` | TypeScript SDK for agent developers | 🚧 In Development |
| `@ClawKit/registry` | Widget Registry client + publishing tools | 📋 Planned |
| `@ClawKit/widgets` | 30+ official built-in widgets | 🚧 In Development |

> **Full architecture doc**: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

---

## LLM Extensibility

ClawKit is designed to work with any LLM. Three mechanisms ensure reliable widget generation:

### 1. Schema-as-Prompt

Every widget ships with an LLM-readable schema summary. Drop it into your system prompt:

```python
from ClawKit import get_widget_prompts

# Get prompt-ready descriptions for selected widgets
prompt_context = get_widget_prompts([
    "ClawKit/map-route",
    "ClawKit/product-carousel",
    "ClawKit/metrics"
])

system_prompt = f"""You are a helpful assistant.
When appropriate, include widgets in your response.

Available widgets:
{prompt_context}
"""
```

### 2. Recommend API

Don't know which widget to use? Let ClawKit decide:

```python
from ClawKit import recommend_widgets

suggestions = recommend_widgets(
    context="User asked about nearby restaurants for dinner",
    max_results=3
)
# Returns: [
#   {"type": "ClawKit/map-list", "confidence": 0.92},
#   {"type": "ClawKit/product-carousel", "confidence": 0.78},
#   {"type": "ClawKit/quick-actions", "confidence": 0.71}
# ]
```

### 3. Validate & Fallback

All widget JSON is validated against schemas. On failure, graceful degradation to text:

```python
from ClawKit import validate_widget

result = validate_widget(widget_json)
if not result.valid:
    # Auto-fallback: widget renders as formatted text
    # No crash, no broken UI
    pass
```

---

## Compatibility

ClawKit is designed to coexist with (not replace) the emerging Agent UI ecosystem:

| Protocol | Relationship |
|----------|-------------|
| **AG-UI** (CopilotKit) | ClawKit messages can be transported over AG-UI event streams |
| **A2UI** (Google) | L1 declarative widgets can use A2UI component format internally |
| **MCP Apps** (Anthropic + OpenAI) | ClawKit widgets can wrap MCP App iframes |
| **Open-JSON-UI** (OpenAI) | Compatible schema mapping available |

---

## Roadmap

| Phase | Timeline | Deliverables |
|-------|----------|-------------|
| **P0 — Foundation** | Month 1-2 | Protocol v0.1, React Renderer, 30 built-in widgets, CLI scaffold, 3 killer demos |
| **P1 — Ecosystem** | Month 3-4 | Widget Registry launch, Vue Renderer, Python/TS SDK, third-party publishing |
| **P2 — Intelligence** | Month 5-8 | Recommend API v1, Flutter Renderer, Mini Program Renderer, A2UI/AG-UI bridge |
| **P3 — Scale** | Month 9-12 | Widget composition engine, industry template marketplace, Enterprise edition |

---

## Contributing

We welcome contributions of all kinds! See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for details.

**Especially looking for:**

- 🎨 **Widget developers** — Build widgets and publish to Registry
- 🔧 **Renderer developers** — Help build Vue / Flutter / Mini Program renderers
- 🧪 **Agent developers** — Try ClawKit in your agent and give feedback
- 📖 **Documentation** — Improve docs, write tutorials, translate
- 💡 **Ideas** — Open issues with your use cases and widget ideas

### Development Setup

```bash
git clone https://github.com/user/ClawKit.git
cd ClawKit
pnpm install        # Install all dependencies
pnpm dev            # Start development server
pnpm test           # Run tests
pnpm build          # Build all packages
```

### Project Structure

```
ClawKit/
├── packages/
│   ├── protocol/       # JSON Schema definitions & TypeScript types
│   ├── core/           # Protocol parser, validator, widget resolver
│   ├── react/          # React Renderer
│   ├── vue/            # Vue Renderer (planned)
│   ├── widgets/        # 30+ official built-in widgets
│   └── sdk/            # TypeScript SDK for agent developers
├── python/
│   └── ClawKit/        # Python SDK
├── apps/
│   ├── demo/           # Demo application (4 scenarios)
│   ├── registry/       # Widget Registry server
│   ├── playground/     # Interactive widget playground
│   └── docs/           # Documentation site
├── docs/               # Project documentation
│   ├── PROTOCOL.md     # Protocol specification
│   ├── ARCHITECTURE.md # Technical architecture
│   ├── WIDGET_CATALOG.md  # Full widget reference
│   └── CONTRIBUTING.md # Contribution guide
└── examples/
    ├── legal-advisor/  # Legal consultation demo
    ├── shopping/       # E-commerce assistant demo
    ├── travel/         # Travel planning demo
    └── analytics/      # Data analytics demo
```

---

## Community

- 💬 [Discord](https://discord.gg/ClawKit) — Chat with the team and community
- 🐦 [Twitter](https://twitter.com/ClawKit) — Updates and announcements
- 📝 [Blog](https://ClawKit.dev/blog) — Deep dives and tutorials
- 🐛 [Issues](https://github.com/user/ClawKit/issues) — Bug reports and feature requests

---

## License

ClawKit is open source under the [Apache License 2.0](LICENSE).

The core protocol, all renderers, built-in widgets, and SDKs are **free forever**.

---

<p align="center">
  <strong>ClawKit — Let every Agent speak GUI.</strong><br/>
  <sub>Built with ❤️ for the Agent-native future.</sub>
</p>
