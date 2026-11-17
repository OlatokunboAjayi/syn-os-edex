<p align="center">
  <img alt="Syn OS Logo" src="media/logo.png" width="120"><br><br>
  <strong>SYN OS — EDEX</strong><br>
  <em>Neural Operating System · Sci-Fi Command Interface</em>
</p>

---

**syn-os-edex** is the Svelte/TypeScript frontend shell for [Syn OS](https://github.com/OlatokunboAjayi/syn-os) — a fully realized, sci-fi cyberpunk command center running in Electron (desktop) or the browser. Built on top of the eDEX-UI aesthetic, it integrates directly with the Syn OS backend for real-time AI, security, GIS, and device management.

---

## ✨ What's Inside

### 🖥️ Command Center Dashboard
Seven tabs, all live-connected to the Syn OS backend via REST + WebSocket:

| Tab | Icon | Description |
|-----|------|-------------|
| Task Orchestrator | ◉ | Submit and monitor ML-scheduled tasks |
| Security Center | ⬢ | Live threat monitoring, anomaly scores, scan results |
| Threat Intel | ⚠ | Live IOC feed, severity filter, IP/domain checker |
| Geospatial Intel | ⌖ | Outdoor Leaflet map + Indoor floor-plan overlay |
| Devices | 📡 | Register, ping, and manage network devices |
| ML Optimization | ◆ | Model status, training metrics, forecasts |
| Cluster Status | ⬡ | Node health and task distribution |

### 🎙️ Voice Commands *(NEW)*
No external service — uses the browser's built-in **Web Speech API**.

Click the 🎤 mic button in the nav bar, then say:

| Voice command | Result |
|---------------|--------|
| `Synapse, run scan` | → Task Orchestrator |
| `Synapse, threat feed` | → Threat Intel tab |
| `Synapse, devices` | → Device Manager tab |
| `Synapse, geo` | → Geospatial HUD |
| `Synapse, security` | → Security Center |
| `Synapse, stop` | Disable voice |

Status shown in bottom bar: **VOICE: ACTIVE / OFF / N/A**

### 🗺️ Geospatial HUD
- **Outdoor mode** — dark-mode Leaflet map with live device markers and LSTM-predicted paths
- **Indoor mode** — upload floor plans, pin device locations, live WebSocket updates

### ⚠️ Threat Intelligence *(NEW)*
- Scrolling IOC feed polled every 30 seconds
- Filter by severity: Critical · High · Medium · Low
- Inline checker: type any IP or domain to see if it's flagged

### 📡 Device Manager *(NEW)*
- Sortable device table: name, IP, type, status (🟢/🔴/⚪), last-seen
- Add new devices via form
- Ping → updates status live
- Remove button per row

---

## 🏗️ Project Structure

```
syn-os-edex/
├── electron/                  # Electron main process
│   └── main.js
├── src/
│   ├── App.svelte             # Root shell (Electron window + mount)
│   ├── main.ts                # Vite entry point
│   ├── components/
│   │   └── synos/
│   │       ├── CommandCenter.svelte   # Tab shell + voice wiring
│   │       ├── SystemMetrics.svelte   # CPU/RAM/Net sidebar
│   │       ├── TaskOrchestrator.svelte
│   │       ├── SecurityMonitor.svelte
│   │       ├── ThreatIntel.svelte     # IOC feed UI        ← NEW
│   │       ├── GeoDashboard.svelte    # Outdoor map
│   │       ├── IndoorMap.svelte       # Floor plan overlay
│   │       ├── DeviceManager.svelte   # Device CRUD UI     ← NEW
│   │       ├── MLOptimization.svelte
│   │       └── ClusterStatus.svelte
│   ├── modules/
│   │   └── synos/
│   │       ├── config.ts      # Backend URL config
│   │       ├── init.ts        # API + WebSocket init
│   │       └── voice.ts       # VoiceController (Web Speech) ← NEW
│   └── stores/
│       └── synos/
│           ├── client.ts      # synosClient (REST helper)
│           └── kernel.ts      # cpu/memory/network stores
├── media/                     # Icons and logos
├── synos.config.json          # Syn OS backend URL config
├── package.json
├── svelte.config.mjs
├── vite.config.mjs
└── tsconfig.json
```

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Running [Syn OS backend](https://github.com/OlatokunboAjayi/syn-os) on port 8000

### Development (browser)
```bash
git clone https://github.com/OlatokunboAjayi/syn-os-edex.git
cd syn-os-edex
npm install
npm run dev
# → opens at http://localhost:5173
```

### Desktop (Electron)
```bash
npm run electron:dev    # hot-reload dev mode
npm run electron:build  # build distributable
```

### Configuration
Edit `synos.config.json` to point at your backend:
```json
{
  "apiUrl": "http://localhost:8000/api/v1",
  "wsUrl": "ws://localhost:8000"
}
```

---

## 🎙 Voice Command Reference

| Category | Say | Action |
|---------|-----|--------|
| Navigation | `Synapse, run scan` | Task Orchestrator |
| | `Synapse, metrics` | Task Orchestrator |
| | `Synapse, security` | Security Center |
| | `Synapse, threat feed` | Threat Intel |
| | `Synapse, geo` | Outdoor map |
| | `Synapse, indoor` | Indoor mode |
| | `Synapse, devices` | Device Manager |
| Control | `Synapse, stop` | Disable voice |

> Works in **Chrome / Edge / Electron** (Web Speech API required). Firefox not supported.

---

## 🔗 Related

- **[syn-os](https://github.com/OlatokunboAjayi/syn-os)** — Backend (Rust kernel + Python ML + FastAPI)

---

## 📄 License

GPLv3 — see [LICENSE](LICENSE)

> *Built on the shoulders of [eDEX-UI](https://github.com/GitSquared/edex-ui) by GitSquared*
