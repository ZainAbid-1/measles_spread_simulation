# Simulating Measles Spread in Social Networks

A high-speed, live simulation engine built to model and visualize the propagation of measles. The project integrates real-world contact data with a dual-transmission model, accounting for both physical touch and airborne viral loads (The Invisible Cloud) via an environmental Air Quality Index (AQI).

---

### 📦 Stack

- **React.js** (Frontend & HTML5 Canvas rendering)
- **FastAPI** (Python Backend)
- **WebSockets** (Low-latency live data streaming)
- **NetworkX** (Graph topology & community detection)
- **SocioPatterns** (Empirical face-to-face contact dataset)

---

### ✨ Quick start

```bash
# Install backend dependencies and start the engine
pip install fastapi uvicorn networkx pandas
uvicorn main:app --reload

# Start the interactive dashboard
npm install
npm run dev
```

The simulation will visualize disease propagation at a smooth **30 FPS** using a cached Archipelago Layout.

---

### 🚀 Simulation Features

- **Real-World Data** — Utilizes 20-second granular time-series data from SocioPatterns for authentic human behavior modeling.
- **Airborne (AQI) Model** — An "environmental memory" model where infectious individuals shed particles into zones, subject to live ventilation rates.
- **Archipelago Layout** — A customized Fruchterman-Reingold visualization that delineates social communities as distinct "islands."
- **Performance Optimized** — Leverages **QuadTrees** for spatial indexing and **heapq** for Discrete Event Simulation (DES) management.

---

### 🎹 Controls

- **Sickness Parameters** — Adjust Transmission Rate ($\beta$), Recovery Time ($\gamma$), and Initial "Patient Zero" count.
- **Air Quality Sliders** — Live-tweak Ventilation Rate ($V_{rate}$), Air Infectivity, and Viral Shedding Rate.
- **Analytics Dashboard** — Real-time tracking of SEIRD population curves, $R_0$ calculations, and Transmission Vector breakdowns.

---

### 🤖 How it works

The simulation pipeline operates through a four-phase streaming architecture:

1.  **Preprocessing** — Louvain Community Detection identifies social districts; a Constrained Spring Embedder generates the fixed Archipelago coordinates.
2.  **DES Engine** — A Discrete Event Simulation processes temporal contacts. New infections are determined probabilistically ($P = 1.0 - e^{-\beta_{air} \cdot AQI}$).
3.  **Environmental Decay** — Each time step, viral loads diminish based on the formula: $AQI \leftarrow AQI \times (1 - V_{rate})$.
4.  **Streaming** — FastAPI yields JSON "Step" packets via WebSockets to a React `useRef` hook, bypassing slow re-renders for fluid Canvas visualization.

---

### 📁 Project structure

```
src/
  frontend/
    components/        # HTML5 Canvas and QuadTree visualization logic
    hooks/             # WebSocket management and useRef memory store
  backend/
    measles_model/     # DES engine and probabilistic transmission logic
    data_loader/       # SocioPatterns parsing and Louvain clustering
    api/               # FastAPI WebSocket endpoints
  data/                # Real-world contact network datasets
```

---

### 👤 Authors

**Zain Abid (507257), M. Haad Rehman (501714), & M. Faiq Abdullah (510682)** — Simulation & Modeling Project
