---
status: legacy_do_not_use_as_truth
legacy_marked_at: 2026-05-12
supersedes: C:\dev\Investigacion_Osla_consolidada\OK\modulos\osla_puerto\product.md
reason: OSLA canonical documentation moved to consolidated OK tree after V3/saneamiento audit.
do_not_use_for: product_truth, roadmap_truth, implementation_scope, claims, data_rights
---

# AGENTS.md — OslaPuerto

## Identidad del proyecto

- **Nombre**: OslaPuerto (Inteligencia Portuaria UY)
- **Ranking InvestigaVert**: — Score 4.0)
- **AshRise project_id**: `puerto`
- **Puerto Postgres**: 5455
- **DB**: puerto / user: puerto
- **ICP primario**: Freight forwarders
- **ICP secundario**: Operadores portuarios, shipping lines
- **Pricing target**: USD 300-500/usuario/mes
- **Estado validación**: PENDIENTE — requiere validación con operadores

## Qué es

Módulo de logística portuaria que integra AIS tracking (posición buques en tiempo real) + NOAA weather (predicción 15 días) + ECMWF (clima marítimo) + DNA (carga) + congestión histórica. ETA prediction, berth scheduling optimization, alertas de demoras y reencaminamientos. Sistema que reduce esperas portuarias e impide bloqueos de carga.

## Problema que resuelve

Forwarder tiene contenedor llegando Montevideo el jueves, pero no sabe si puerto está congestionado. Hoy: llama operador, espera, o pierde deadline. Un sistema que predice ETA con 95%+ accuracy, sugiere berth óptimo, y alerta con 48 horas anticipación convierte la incertidumbre logística en certeza operacional.

## Modelos ML defensibles

1. **Vessel ETA Prediction** (XGBoost): predice hora de arribo con MAPE <0.5%.
2. **Berth Scheduling Optimization** (Mixed Integer Programming): asigna muelles minimizando espera.
3. **Congestion Forecasting** (LSTM): predice congestión portuaria 7 días adelante.
4. **Weather Risk Detection** (ECMWF ensemble): alerta si condiciones marítimas amenazan operación.

## Fuentes de datos

### Uruguay
- ANP: datos portuarios (requiere contacto directo)
- DNA: datos de carga, destinos, horarios
- BCU: cotizaciones USD/EUR con conversión
- IMPO API: aranceles (impacto en documentación)

### Internacionales
- Marine Cadastre AIS (NOAA, regional/histórico): posiciones satélites buques
- NOAA (CC0): datos meteorológicos, predicción 15 días
- ECMWF (CC BY 4.0): datos climáticos marítimos + forecast
- UN/LOCODE: códigos puertos mundo
- World Port Index: información puertos globales
- SMDG: normas contenedores
- BIC Facility Codes: instalaciones portuarias
- DCSA (API estándar): datos de carga estandarizado
- VesselFinder / MarineTraffic: AIS real-time global (capa paga)

## Acceso a datos compartidos (via FDW)

```sql
SELECT * FROM shared.entity WHERE ...;
SELECT * FROM shared.fx_rates WHERE currency_code = 'USD';
```

## Stack técnico

- Backend: FastAPI (Python)
- Frontend: Next.js 15 + Tailwind
- DB: Postgres 16 (puerto 5455)
- ML: scikit-learn + XGBoost + LightGBM + PyTorch LSTM
- Optimización: OR-Tools (Google)
- Mapping: Mapbox + Folium
- Storage: S3-compatible
- Queue: Redis (para tracking AIS real-time)

## Reglas de boundary

1. Repo, base de datos, storage y colas propios.
2. No leer ni escribir directo en la base de otra vertical.
3. Compartir datos solo por FDW read-only desde shared-db.
4. Reusar patrones del núcleo reusable (source discovery, document extraction, identity resolution, alerts/tasks).

## Reglas para agentes

1. **No escribir en shared-db** — solo leer vía FDW
2. **AIS + NOAA es fuente de verdad** para condiciones marítimas
3. **Evidence-first**: cada predicción deja track AIS, condiciones, confianza
4. **Deterministic-first**: usar ML pero validar con modelo hidronáutico simple
5. **No afirmar retraso sin evidencia de congestión u obstáculo climático**

## Variables de entorno

```
ASHRISE_BASE_URL=http://localhost:8080
ASHRISE_TOKEN=<token>
ASHRISE_PROJECT_ID=puerto
NOAA_KEY=<key>
ECMWF_KEY=<key>
```

## Documentación del producto

- **[docs/Producto.md](docs/Producto.md)** — Documento completo del producto: visión, ICP, propuesta de valor, fuentes de datos, modelos ML, competencia, arquitectura, roadmap y métricas. Se actualiza cuando una investigación impacta esta vertical.
- **[docs/Investigaciones.md](docs/Investigaciones.md)** — Log cronológico de investigaciones procesadas que impactan esta vertical: si fortalecen o debilitan la tesis, y qué se actualizó en Producto.md como consecuencia.
- **[docs/ROADMAP.md](docs/ROADMAP.md)** — Milestones técnicos de implementación.

## Contrato AshRise

Al iniciar sesión: leer AGENTS.md → docs/ROADMAP.md → GET /state/puerto → GET /handoffs/puerto?status=open
Al cerrar: emitir ashrise-close con run + state_update.

## Nota especial

AIS global real-time requiere suscripción a VesselFinder o MarineTraffic. MVP funciona con histórico NOAA + posiciones periódicas.
