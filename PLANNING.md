# ⚙️ LatencyLens

> "Visual and intelligent latency and trace inspector for distributed systems"

## 🧠 What is LatencyLens?

A tool that consumes distributed traces (like OpenTelemetry, Jaeger, Zipkin), analyzes them, and provides visual insights about:
- Service bottlenecks
- Average latency per endpoint
- Slow call trees
- Temporal analysis (when something became slow)
- Recommendations (with or without AI) to improve architecture

## 🧰 Proposed Tech Stack

### Backend
- **Go** – for trace processing
- **OpenTelemetry Collector** – optional if you want to simulate a real environment
- **PostgreSQL** – for storing spans if you decide to persist them
- **gRPC/REST API** – to expose processed data

### Frontend
- **Next.js (App Router)** – modern and reactive UI
- **Tailwind + shadcn/ui** – for clean components
- **D3.js** – for visualizations (flamegraph, timelines, heatmaps)
- **Framer Motion** – for professional transitions

## 🧪 MVP: What can it do from the start?

### Input
- JSON trace files (e.g., exported from Jaeger or Zipkin)
- (Phase 2) Real-time collection with OpenTelemetry SDK

### Processing
- Parse spans and group by:
  - Service
  - Operation
  - Response time
  - Trace ID

### Visualization
- Display call trees (Service A → B → C) with latencies
- Identify services with higher TTFB (Time To First Byte)
- Table of slowest endpoints (with latency histograms)

## 🌟 WOW Phase: Advanced Features

1. **"Bottleneck Highlight"**
   - Automatically color services that exceed certain p95 latency

2. **"Recommendations" (AI or heuristics)**
   - Type: "This service chain has high fan-out and could benefit from batching"

3. **Interactive Timeline**
   - Filter by time of day and see changes in latency or throughput

4. **Automatic Trace Import**
   - From Cloud Run, GCP, etc. (if you want to make it more realistic)

## 🧱 Repository Structure (initial proposal)

```
latencylens/
├── backend/
│   ├── main.go
│   ├── parser/          # Zipkin/Jaeger JSON parsers
│   ├── analysis/        # Bottlenecks, rankings
│   ├── models/          # Span, Trace, Endpoint, etc.
│   └── api/             # REST/gRPC endpoints
├── frontend/
│   ├── app/             # Next.js App Router
│   ├── components/
│   ├── lib/
│   └── pages/
├── data/
│   └── example-traces/
├── docs/
│   └── screenshots.md
└── README.md
```

## 🧭 Roadmap in 3 phases

### ✅ Phase 1: Basic MVP
- Trace file parser (Zipkin/Jaeger)
- Total latency calculation per trace
- UI for loading traces and viewing call trees
- Table of slowest endpoints sorted

### 🚀 Phase 2: Analysis + Visuals
- Interactive flamegraph
- Bottleneck highlighting
- Time/service filters

### 🤯 Phase 3: Smart Recommendations
- Automatic heuristics (e.g., fan-out, retries, cascades)
- GPT integration for semantic suggestions
- Export reports in Markdown or PDF

## ✅ What skills does this project demonstrate?
- Performance-oriented backend architecture
- Observability/infra data handling
- Advanced data visualization
- Clean UI with good dev experience
- Optional AI integration as added value