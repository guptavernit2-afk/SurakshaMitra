# SurakshaMitra 🛡️ | Tactical Digital Twin for Industrial Disasters

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Python](https://img.shields.io/badge/python-3.9+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-009688.svg?logo=fastapi)
![MapLibre](https://img.shields.io/badge/MapLibre-WebGL-FF814A?logo=maplibre)
![SIH 2026](https://img.shields.io/badge/SIH_2026-Problem_SIH260205-orange)

**Smart India Hackathon 2026** | **Problem Statement:** SIH260205 | **Ministry of Home Affairs (MHA)**

**SurakshaMitra** is a live, physics-driven tactical digital twin designed for Incident Commanders. In the event of a catastrophic chemical or hydrocarbon vessel breach, commanders have less than 15 minutes to make critical staging and evacuation decisions. SurakshaMitra replaces static PDF emergency plans with real-time, mathematically grounded disaster containment directives in milliseconds.

---

## ⚡ Core Tactical Capabilities

1. **Domino Cascade Defense:** Continuously calculates point-source thermal flux on adjacent storage vessels. Triggers automated high-volume cooling alerts the millisecond radiant heat breaches the critical structural threshold ($15.0\text{ kW/m}^2$).
2. **Automated Gate Alpha Ingress:** Evaluates facility perimeter gates using threat geometry and downwind dot-products to pinpoint the safest upwind entry point ($\le 1.6\text{ kW/m}^2$) for fire tenders.
3. **Threat-Zone Avoidance Triage:** Scans nearby healthcare facilities, drops those trapped inside toxic plumes, and plots dynamic detour corridors for ambulances.
4. **Live SCADA Telemetry Stream:** Dynamically shrinks threat rings in real-time as simulated burn-off reduces active fuel mass ($50,000\text{ kg/tick}$).
5. **Air-Gapped Resilience:** Operates on a 3-Tier Fallback architecture (Cloud APIs ➔ Edge Cache ➔ 100% Client-Side JS) ensuring the system remains operational even if local telecom grids collapse.

---

## 🔬 The Physics & Thermodynamic Engine

Rather than rendering arbitrary hazard circles, the engine computes threat geometries using peer-reviewed industrial explosion models. To eliminate spatial distortion caused by Earth's curvature, all geometric calculations are performed in a local **Azimuthal Equidistant (AEQD)** metric projection before rendering.

* **Overpressure & Hopkinson-Cranz Scaling:** Normalizes fuel types (LPG, Crude, Petrol) into TNT equivalents to project calibrated overpressure destruction tiers.
  * $R = k \cdot W_{TNT}^{1/3}$
* **Thermal BLEVE Fireball Correlation (Roberts'):** Validated against industrial disaster records to compute the maximum thermal radiation envelope before structural fragmentation.
  * $R_{fireball} = 3.86 \cdot m^{0.325}$
* **Point-Source Radiant Heat Flux:** 
  * $q'' = \frac{Q}{4\pi d^2}$ (Alert triggered at $\ge 15.0\text{ kW/m}^2$)
* **$32^\circ$ Rocket-Rupture Shrapnel Projection:** Models vessel geometry (e.g., cylindrical bullets vs. Horton spheres) to calculate directional blast fragment hazard corridors.
* **Atmospheric Plume Dynamics:** Ingests live wind vectors via Open-Meteo to elongate downwind dispersion plumes and compute flame-tilt shadows upwind.

---

## 💻 Tech Stack

* **Frontend:** MapLibre GL JS (WebGL 60FPS), Turf.js (Spatial Math), Vanilla HTML5/CSS3/JS (Zero-build deployment for maximum reliability).
* **Backend:** FastAPI (Python), Uvicorn.
* **Geospatial Processing:** PostGIS/PostgreSQL (Target architecture), AEQD metric conversions.
* **APIs:** Open-Meteo (Live Wind Data), OSRM (Dynamic Triage Routing).
* **Deployment:** Render (Live API), Vercel/GitHub Pages (Static Client).

---

## 📌 Key Validation Case: Jaipur IOCL Fire (October 2009)

* **Facility:** Jaipur Indian Oil Corporation Ltd. (IOCL) Terminal (`26.8505° N, 75.8069° E`)
* **Fuel Profile:** LPG (TNT Equivalence Factor: 0.70)
* **Initial Mass:** 2,700,000 kg (2.7 Kilotons equivalent)
* **Computed Threat Zones:**
  * **Lethal Zone (> 83 kPa):** ~272 meters (Total structural destruction)
  * **Severe Zone (> 34 kPa):** ~433 meters (Heavy structural damage)
  * **Moderate Zone (> 7 kPa):** ~841 meters (Glass breakage & minor damage)
  * **Fireball Radius:** ~475 meters

---

## 🛠️ Project Architecture

```text
SurakshaMitra/
├── backend/
│   ├── main.py                # FastAPI engine (Handles dynamic zone calculation)
│   ├── generate_fallback.py   # Generates offline Edge-Cache datasets
│   ├── models/
│   │   ├── __init__.py
│   │   ├── blast.py           # TNT Equivalence & Hopkinson-Cranz models
│   │   └── thermal.py         # Point-Source Flux & BLEVE correlations
│   └── requirements.txt       # Python environment dependencies
├── frontend/
│   ├── index.html             # MapLibre GL JS + Turf.js UI (No npm build required)
│   └── data/
│       └── jaipur_demo.json   # Air-gapped fallback GeoJSON payload
└── README.md                  # Documentation
```

---

## 🚀 Quickstart Guide

### 1. Install Backend Dependencies
Ensure you have Python 3.9+ installed.
```bash
pip install -r backend/requirements.txt
```

### 2. Generate Fallback Dataset (Optional)
Run the generator script to populate `frontend/data/jaipur_demo.json`:
```bash
python -m backend.generate_fallback
```

### 3. Start FastAPI Backend
Launch the API server with Uvicorn:
```bash
uvicorn backend.main:app --reload
```
The API server will run at `http://localhost:8000`. Interactive API documentation is available at `http://localhost:8000/docs`.

### 4. Open Frontend
Simply open `frontend/index.html` in your web browser (double click or open via browser).

> **Offline Fallback Feature:** If the FastAPI backend server is not running or unreachable, the frontend automatically and silently loads the pre-baked `frontend/data/jaipur_demo.json` file so you can demonstrate the Jaipur IOCL case offline without any setup!

---

## 🏢 National Scale Validation Presets

The platform is pre-configured with geospatial bounding boxes for major Indian critical infrastructure:
1. **Jaipur IOCL** — `26.8505° N, 75.8069° E` (LPG)
2. **Vizag HPCL** — `17.6868° N, 83.2185° E` (Crude)
3. **Mangalore MRPL** — `12.8916° N, 74.8430° E` (Petrol)
4. **Bina BPCL** — `24.1700° N, 78.1800° E` (LPG)

---

## 🚀 Future Scope & Roadmap

* **Live IoT & SCADA Integration:** Secure edge-connectors to ingest real-time pressure and temperature telemetry from actual plant PLCs.
* **Regulatory Compliance Reporting:** Automated generation of Quantitative Risk Assessment (QRA) reports aligned with OISD (Oil Industry Safety Directorate) and NFPA guidelines.
* **3D Terrain & Urban Rendering:** Leveraging MapLibre's 3D terrain to model how hills and dense urban structures block or channel toxic gas plumes.

---
*Built with precision by Team SurakshaMitra (Krish Baghel, Vernit Gupta, Namrata Kumari, Taniska Bimal, Prem Gopal Soni, Pratyusha Biswas) for SIH 2026.*
