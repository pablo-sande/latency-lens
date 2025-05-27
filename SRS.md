# Software Requirements Specification (SRS) - LatencyLens

**Project:** LatencyLens  
**Author:** Pablo  
**Date:** May 24, 2025  
**Version:** 1.0 (draft)

## 1. Introduction

### 1.1 Purpose
The purpose of this document is to define the functional and non-functional requirements of the LatencyLens system, a distributed trace analysis and visualization tool for detecting bottlenecks in microservices architectures.

This system will be useful for developers, SRE teams, and DevOps engineers who want to improve the observability of their services' performance through detailed analysis of spans collected by tools like OpenTelemetry, Zipkin, or Jaeger.

### 1.2 Scope
LatencyLens will allow users to:
- Upload JSON traces (OpenTelemetry, Zipkin, or Jaeger format)
- Visualize call trees and flamegraphs
- Automatically detect services/endpoints with anomalous latencies
- Generate performance reports and improvement suggestions (manual or AI-assisted)
- Run in local mode (standalone) with future cloud deployment support

### 1.3 Definitions, Acronyms, and Abbreviations

| Term | Definition |
|------|------------|
| Span | An event within a distributed trace |
| Trace | Set of related spans by context |
| p95/p99 | Latency percentiles |
| Flamegraph | Call hierarchy visualization |
| OTel | OpenTelemetry, observability standard |
| LLM | Large Language Model (generative AI) |
| SLO | Service Level Objective |
| MVP | Minimum Viable Product |

### 1.4 References
- OpenTelemetry Specifications
- IEEE 830 Software Requirements Specification
- Zipkin Data Model

## 2. General Description

### 2.1 Product Perspective
LatencyLens will be a modular web application composed of:
- Frontend interface (Next.js)
- Backend API (Go)
- Analysis and visualization engine
- Local storage (PostgreSQL)

### 2.2 Features

| ID | Feature |
|----|---------|
| F1 | Upload JSON traces (OpenTelemetry, Zipkin, or Jaeger) |
| F2 | Parse and store traces in database |
| F3 | Visualize call tree by service and endpoint |
| F4 | Calculate total latencies, p95, p99, fan-out, etc. |
| F5 | Detect and highlight slow or problematic spans |
| F6 | Export report in HTML, Markdown, and PDF |
| F7 | Recommend endpoint improvements (future phase) |

### 2.3 User Characteristics
- **SREs:** Want to visualize bottlenecks and generate latency reports
- **Backend Developers:** Want to understand service relationships and why an endpoint is slow
- **Platform Engineers:** Seek to automate problem detection at the architecture level

### 2.4 Constraints
- The MVP will run in local mode without multi-user support
- Plain JSON formats will be used for input
- Corrupted or malformed traces will not be accepted

### 2.5 Assumptions and Dependencies
- Users already have traces generated and exported in JSON
- Environments where the system runs have Go ≥1.21 and Node.js ≥18
- Standard trace structure according to OpenTelemetry/Zipkin will be assumed

## 3. Specific Requirements

### 3.1 Functional Requirements

| ID | Functional Requirement |
|----|------------------------|
| RF1 | The system must accept JSON files up to 10MB |
| RF2 | The system must identify the root service of each trace |
| RF3 | The system must calculate the total duration of each trace |
| RF4 | The system must display a hierarchical call tree per trace |
| RF5 | The system must generate p95/p99 latency insights |
| RF6 | The system must allow filtering by service, endpoint, and duration |
| RF7 | The system must allow exporting visualizations to PDF |

### 3.2 Non-Functional Requirements

| ID | Non-Functional Requirement |
|----|----------------------------|
| RNF1 | The system must load a 10MB trace in less than 1 second |
| RNF2 | The UI must be responsive and accessible from mobile devices |
| RNF3 | The backend must expose Prometheus metrics at /metrics |
| RNF4 | The system must be able to run in a Docker container |
| RNF5 | The system must function offline without internet connection |
| RNF6 | The system must have at least 80% test coverage |

### 3.3 External Interfaces

| Interface | Description |
|-----------|-------------|
| JSON API | REST API for uploading traces and querying analysis |
| Web UI | Next.js frontend with interactive components |
| Input File | JSON format compatible with Zipkin or Jaeger |
| Exporter | PDF/HTML report generator using Puppeteer or similar |

## 4. Appendices

### 4.1 Expected Input Format (Zipkin JSON example)

```json
[
  {
    "traceId": "abcdef",
    "id": "123456",
    "name": "getUser",
    "timestamp": 1685570281000000,
    "duration": 50000,
    "localEndpoint": {
      "serviceName": "user-service"
    }
  }
]
```

### 4.2 Proposed Technology Stack
- **Frontend:** Next.js, Tailwind, d3.js
- **Backend:** Go (Gin or Fiber), PostgreSQL
- **Reports:** Puppeteer (Node)
- **Containers:** Docker, docker-compose
