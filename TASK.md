# ✅ TASKS.md – Development Roadmap: LatencyLens

This document details the tasks for developing **LatencyLens**, a web tool for analyzing distributed traces, detecting bottlenecks, and interactively visualizing latencies. Tasks are organized by phases and serve as a technical roadmap.

---

## 🏁 Phase 0: Project Initialization

> This phase establishes the foundation for technical development. Must be completed before starting backend or frontend.

- [ ] Create Git repository (GitHub or GitLab)
- [ ] Add initial documentation:
  - [ ] `README.md` with project overview
  - [ ] `docs/SRS.md` with requirements document (Software Requirements Specification)
  - [ ] `LICENSE` (MIT recommended)
- [ ] Set up initial folder structure:
/frontend
/backend
/docs
/samples
- [ ] Initialize development environment:
- [ ] Backend with Go (`go mod init`)
- [ ] Frontend with Next.js (`npx create-next-app@latest`)
- [ ] Docker for PostgreSQL (see Phase 5)
- [ ] Create `.env` file for local configuration

---

## 🛠️ Phase 1: Backend - Trace ingestion and analysis

**Suggested language:** Go  
**Database:** PostgreSQL

### 📁 Module: JSON Ingestion
- [ ] Design interface for generic parser (`interface TraceParser`)
- [ ] Implement Zipkin format parser
- [ ] Implement Jaeger parser (optional MVP+)
- [ ] Validate input files and size (max 10MB)

### 🧮 Module: Trace Analysis
- [ ] Model data structures: `Span`, `Trace`, `ServiceNode`
- [ ] Build call tree by `traceId`
- [ ] Calculate total duration, fan-out, maximum depth
- [ ] Calculate p50, p95, p99 latencies per endpoint
- [ ] Detect spans with anomalous latencies

### 🛢️ Module: Storage
- [ ] Configure PostgreSQL connection with `pgx` or `gorm`
- [ ] Define basic models and migrations
- [ ] Create indexes for searching by `traceId`, `service`, `duration`

---

## 🌐 Phase 2: REST API

**Suggested framework:** Gin

- [ ] `POST /upload` endpoint for JSON file upload
- [ ] `GET /traces` endpoint to list processed traces
- [ ] `GET /traces/:id` endpoint to query details
- [ ] `GET /metrics` endpoint for Prometheus integration
- [ ] Add middlewares for:
- [ ] Structured logging
- [ ] CORS
- [ ] Error handling and recovery
- [ ] Basic endpoint tests with `httptest`

---

## 🎨 Phase 3: Frontend

**Suggested framework:** Next.js + TailwindCSS

### 📄 Basic UI
- [ ] File upload screen (drag & drop)
- [ ] Traces table with duration, services, and date
- [ ] Detailed view with hierarchical call tree

### 🔥 Flamegraph
- [ ] Integrate `d3-flame-graph` or `flamegraph.js`
- [ ] Visualize duration per span with latency-based colors
- [ ] Tooltip with service name, endpoint, and duration

### 📤 Export
- [ ] Button to export visual report to PDF (using Puppeteer or `react-pdf`)

---

## 🧠 Phase 4 (optional MVP+): AI-assisted Analysis

- [ ] Generate natural language summary of bottlenecks
- [ ] Add LLM integration:
- [ ] Local option (`ollama`, `llama.cpp`)
- [ ] Cloud option (`OpenAI`, `Gemini`, `Claude`)
- [ ] Generate improvement recommendations for slow traces

---

## ⚙️ Phase 5: DevOps & Tooling

- [ ] Create `Dockerfile` for backend
- [ ] Create `docker-compose.yml` with:
- [ ] Backend (Go)
- [ ] Frontend (Next.js)
- [ ] PostgreSQL
- [ ] Configure basic CI/CD (GitHub Actions or similar)
- [ ] Test coverage:
- [ ] Backend: `go test -cover`
- [ ] Frontend: `jest --coverage`
- [ ] Add linters and formatters:
- [ ] Backend: `golangci-lint`
- [ ] Frontend: `eslint`, `prettier`

---

## 📈 Phase 6: QA and stress testing

- [ ] Create test trace set (`/samples/*.json`)
- [ ] Load large files (>500 spans) for benchmarking
- [ ] Validate mobile UX and screen reader compatibility
- [ ] Verify OpenTelemetry format compatibility

---

## 🧪 Bonus ideas (stretch goals)

- [ ] Auto-detect anomalies with clustering or heuristic rules
- [ ] Multi-user support with basic authentication (JWT + login)
- [ ] Prometheus/Grafana exporter for analysis metrics
- [ ] CLI tool for offline terminal analysis

---

