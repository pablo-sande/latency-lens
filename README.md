# LatencyLens

Visual and intelligent latency and trace inspector for distributed systems.

## Overview
LatencyLens is a tool for analyzing distributed traces (OpenTelemetry, Jaeger, Zipkin), providing visual insights into service bottlenecks, latency, and call trees. It helps SREs, developers, and platform engineers understand and improve the performance of microservices architectures.

## Features
- Upload and parse JSON traces (OpenTelemetry, Zipkin, Jaeger)
- Visualize call trees and flamegraphs
- Detect and highlight slow or problematic spans
- Calculate latency percentiles (p95, p99)
- Export performance reports (HTML, PDF)
- (Future) AI-powered recommendations for improvements

## Tech Stack
- **Backend:** Go, PostgreSQL, REST/gRPC API
- **Frontend:** Next.js, Tailwind, D3.js
- **DevOps:** Docker, GitHub Actions

## Repository Structure
```
latency-lens/
├── backend/         # Go backend (parsing, analysis, API)
├── frontend/        # Next.js frontend (UI, visualizations)
├── data/            # Example traces and data
├── docs/            # Documentation and screenshots
├── samples/         # Sample trace files
├── tests/           # Unit and integration tests
├── PLANNING.md      # Architecture and planning
├── SRS.md           # Software Requirements Specification
├── TASK.md          # Task and progress tracking
└── README.md        # This file
```

## Getting Started
1. Clone the repository
2. See `PLANNING.md` and `SRS.md` for requirements and architecture
3. Follow setup instructions for backend and frontend (coming soon)

## License
MIT (see LICENSE)
