# ROADMAP — OslaPuerto (Inteligencia Portuaria UY)

## Estado actual

MVP conceptual. Requiere integración AIS + NOAA + ECMWF + DNA + ANP. ML para ETA prediction y berth optimization.

---

## Roadmap integrado

### Fase 1 — ETA Prediction MVP (semanas 1-10)

**Entidades canónicas:**
- Buque (MMSI, AIS)
- Contenedor (BL, DNS, DNA)
- Puerto (LOCODE, SMDG code)
- Muelle (berth, facility code)
- Condiciones (NOAA weather, ECMWF forecast)
- Operación (carga, descarga, demora)

**Milestones:**
- **M1:** AIS data pipeline (Marine Cadastre NOAA, histórico)
- **M2:** NOAA weather integration (current + 15-day forecast)
- **M3:** ECMWF climate data (ocean state, wind)
- **M4:** DNA carga integration (container manifests)
- **M5:** XGBoost ETA prediction model (MAPE <0.5%)
- **M6:** Congestion forecasting (LSTM 7-day horizon)
- **M7:** Product surface `/product/vessel/` (tracking explorer)
- **M8:** Dashboard B2B forwarders (realtime tracking + ETA)
- **M9:** Testing + documentation (60+ test cases)
- **M10:** MVP launch con 3-5 forwarders piloto

**ML Pipeline:**
1. Feature engineering: AIS histórico (velocidad, distancia, ruta), NOAA (viento, ola), ECMWF, estacionalidad, muelle congestion histórica
2. ETA prediction (XGBoost + LightGBM ensemble): MAPE <0.5%
3. Congestion forecast (LSTM): RMSE <2 buques/día (7 días)
4. Weather risk (threshold-based NOAA alerts)

**Validation criteria:**
- AIS latency <1h (histórico) | real-time si suscrip pago
- NOAA sync latency <6h
- ETA accuracy MAPE <0.5% (validation set)
- Congestion forecast RMSE <2 buques
- Forwarder adoption (SUS >70)

---

### Fase 2 — Berth Optimization + Scheduling (semanas 10-20)

**Milestones:**
- **M11:** Mixed Integer Programming para berth assignment
- **M12:** Scheduling optimizer (minimize espera, respeta prioridades)
- **M13:** Weather-contingent rescheduling
- **M14:** Integration con ANP (operador real, si cooperan)
- **M15:** API product (/api/v1/port/*)

**ML/Optimization enhancements:**
- OR-Tools para MIP solving
- Reinforcement Learning para policy refinement (opcional)
- Real-time re-optimization

**Validation criteria:**
- Berth assignment latency <100ms
- Schedule feasibility 98%+
- Wait time reduction 15-20% vs baseline
- API latency <500ms

---

### Fase 3 — Network + Regional (semanas 20-30)

**Milestones:**
- **M16:** Multi-port tracking (Punta del Este, Colonia)
- **M17:** Regional network (Buenos Aires, Santos)
- **M18:** Vessel exchange risk (if vessel A delayed, what cargo affected?)
- **M19:** Premium pricing for ETA guarantee

**Validation criteria:**
- Network coverage >5 puertos
- Exchange risk correlation >0.70
- Premium adoption >20% customers

---

### Fase 4 — Scale + Autonomy (meses 6+)

**Milestones:**
- **M20:** Real-time AIS subscription (VesselFinder o MarineTraffic)
- **M21:** Autonomous port communication (Portnet, autoridad portuaria APIs)
- **M22:** Mobile app (captain notifications)

---

## Stack especificación

**Backend:**
```
FastAPI + Pydantic
Postgres 16 con time-series extension
Redis para caching real-time
Airflow para ETL batch
Kafka para AIS stream (opcional, fase 4)
```

**Frontend:**
```
Next.js 15
Mapbox para tracking visual
D3.js + Plotly para analytics
Tailwind CSS
```

**ML & Optimization:**
```
scikit-learn + LightGBM
XGBoost (ETA ensemble)
PyTorch LSTM (congestion)
OR-Tools (Google, scheduling)
statsmodels (seasonality)
```

**Data sources:**
```
Marine Cadastre AIS (NOAA, libre histórico)
NOAA weather (free, real-time)
ECMWF Copernicus (forecast)
DNA API (manifests)
VesselFinder/MarineTraffic (optional, paid AIS)
World Port Index (port data)
SMDG (container standards)
DCSA (shipping API standard)
```

---

## Métricas de éxito

| Métrica | Actual | Target M10 | Target M30 |
|--------|--------|------------|------------|
| Buques rastreados/mes | 0 | 200+ | 2000+ |
| Contenedores tracked | 0 | 5K | 100K+ |
| ETA accuracy (MAPE) | N/A | <0.5% | <0.3% |
| Congestion forecast RMSE | N/A | <2 buques | <1 buque |
| Forwarder users | 0 | 5 | 50 |
| MRR | $0 | $1K | $15K |

---

## Riesgos y mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|--------|-----------|
| ANP no comparte datos reales | Media | Medio | MVP sin ANP, focus forwarders |
| AIS real-time requiere pago | Alta | Bajo | MVP histórico NOAA suficiente |
| NOAA forecast skill variable | Baja | Bajo | Ensemble con ECMWF |
| Competencia DP World / APM | Media | Medio | Defensible: UY monopolio + local operators |
| Regulación privacidad AIS (buques) | Baja | Bajo | AIS es público por definición |

---

## Presupuesto estimado (MVP)

| Línea | Costo | Duración |
|-------|-------|----------|
| Ingeniería (2.5 FTE) | $37K | 6 meses |
| Cloud infra (AWS) | $2K/mes | ongoing |
| NOAA data (libre) | $0 | N/A |
| Testing + forwarder pilots | $4K | 2 meses |
| **Total MVP** | **~$80K** | **6 meses** |

---

## Hitos clave

- **Week 2:** M1 (AIS crítico, start early)
- **Week 6:** M2-M3, NOAA+ECMWF data flowing
- **Week 10:** M4-M5, XGBoost model trained
- **Week 12:** M6-M7, forecasting funcional
- **Week 14:** M8-M9, dashboard público
- **Week 16:** M10, 3-5 forwarders pilotos
