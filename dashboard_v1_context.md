# DASHBOARD PROJECT — LOCKED CONTEXT FILE (V1)

## 🧠 PROJECT SUMMARY
A **local-first, installable dashboard app (Windows first)** that connects to one or more Raspberry Pis via lightweight agents and shows **live system health at a glance**.

This is a **platform foundation**, but V1 is intentionally minimal.

---

## 🔁 CORE LOOP (ONE SENTENCE)
**User opens the dashboard → sees live Raspberry Pi status → immediately knows whether things are healthy.**

If this loop is broken, the app has failed.

---

## 🎯 V1 GOAL
From install → first live metric visible in **under 2 minutes**.

---

## 🏗️ ARCHITECTURE (V1 ONLY)

### Dashboard App
- Tauri (Rust backend)
- React + TypeScript frontend
- Local SQLite database
- Manual device pairing (token-based)
- WebSocket connection for live updates

### Agent (Raspberry Pi)
- Python (FastAPI or equivalent)
- Always-on lightweight process
- Collects basic system metrics
- Streams live data to dashboard

---

## 📡 API CONTRACT (HIGH-LEVEL, LOCKED)

Agent exposes:
- GET /identity
- GET /metrics
- WS /stream

Dashboard:
- Initiates pairing
- Stores trusted devices
- Displays latest metrics only (no history)

(Exact JSON spec is defined separately.)

---

## 🗄️ DATA SCHEMA (LOCKED)

### devices
```
id TEXT PRIMARY KEY
name TEXT
last_seen INTEGER
status TEXT
ip_address TEXT
paired_at INTEGER
```

### metrics_latest
```
device_id TEXT PRIMARY KEY
cpu_percent REAL
mem_used_mb REAL
mem_total_mb REAL
temp_c REAL
updated_at INTEGER
```

### app_settings
```
key TEXT PRIMARY KEY
value TEXT
```

### pairings
```
device_id TEXT PRIMARY KEY
public_key TEXT
paired_at INTEGER
revoked INTEGER
```

---

## 🚧 V1 HARD BOUNDARY (ABSOLUTELY NOT INCLUDED)

- Plugins
- Alerts / notifications
- Logs
- Historical graphs
- File browser
- Service control
- Docker
- GPIO
- Auto-discovery
- Dark mode / themes
- Mobile app
- Cloud sync
- Multi-user
- Accounts / auth systems

---

## ✅ V1 FEATURES (ONLY THESE)

- Windows dashboard app
- Manual pairing with Raspberry Pi agent
- Device list view
- Online / offline status
- Live CPU, RAM, temperature
- Clean, responsive UI
- Local-only operation

---

## 🧭 NEXT EXECUTION STEP
Lock the exact API contract (endpoint paths + JSON payloads).
