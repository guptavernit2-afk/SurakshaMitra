# SurakshaMitra 🛡️ | Tactical Digital Twin for Industrial Disasters

**Smart India Hackathon 2026** | **Problem Statement:** SIH260205 | **Ministry of Home Affairs (MHA)**

**SurakshaMitra** is a live, physics-driven tactical digital twin designed for Incident Commanders. In the event of a catastrophic chemical or hydrocarbon vessel breach, commanders have less than 15 minutes to make critical staging and evacuation decisions. SurakshaMitra replaces static PDF emergency plans with real-time, mathematically grounded disaster containment directives in milliseconds.

---

## ⚡ Core Tactical Capabilities

1. **Domino Cascade Defense:** Continuously calculates point-source thermal flux on adjacent storage vessels. Triggers automated high-volume cooling alerts the millisecond radiant heat breaches the critical structural threshold.
2. **Automated Gate Alpha Ingress:** Evaluates facility perimeter gates using threat geometry and downwind dot-products to pinpoint the safest upwind entry point for fire tenders.
3. **Threat-Zone Avoidance Triage:** Scans nearby healthcare facilities, drops those trapped inside toxic plumes, and plots dynamic detour corridors for ambulances.
4. **Live SCADA Telemetry Stream:** Dynamically shrinks threat rings in real-time as simulated burn-off reduces active fuel mass.
5. **Air-Gapped Resilience:** Operates on a 3-Tier Fallback architecture (Cloud APIs ➔ Edge Cache ➔ 100% Client-Side JS) ensuring the system remains operational even if local telecom grids collapse.

---

## 🔬 The Physics & Thermodynamic Engine

Rather than rendering arbitrary hazard circles, the engine computes threat geometries using peer-reviewed industrial explosion models. To eliminate spatial distortion caused by Earth's curvature, all geometric calculations are performed in a local **Azimuthal Equidistant (AEQD)** metric projection before rendering.

* **Overpressure & Hopkinson-Cranz Scaling:** Normalizes fuel types (LPG, Crude, Petrol) into TNT equivalents to project calibrated overpressure destruction tiers.
  * $R = k \cdot W_{TNT}^{1/3}$
* **Thermal BLEVE Fireball Correlation (Roberts'):** Validated against industrial disaster records to compute the maximum thermal radiation envelope before structural fragmentation.
  * $R_{fireball} = 3.86 \cdot m^{0.325}$
* **Point-Source Radiant Heat Flux:** 
  * $q'' = \frac{Q}{4\pi d^2}$ (Alert triggered at $\ge 15.0\text{ kW/m}^2$ threshold on adjacent tanks)
* **$32^\circ$ Rocket-Rupture Shrapnel Projection:** Models vessel geometry (e.g., cylindrical bullets) to calculate directional blast fragment hazard corridors.

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
│   ├── index.html             # MapLibre GL JS (WebGL) + Turf.js UI (No npm build required)
│   └── data/
│       └── jaipur_demo.json   # Air-gapped fallback GeoJSON payload
└── README.md                  # Documentation
