# Investigaciones — OslaPuerto

> Log cronológico de investigaciones que impactan esta vertical.
> Cada entrada documenta: fuente, fecha, impacto (fortalece/debilita), y qué se actualizó en Producto.md.

---

<!-- FORMATO DE ENTRADA:

## [YYYY-MM-DD] — Título de la investigación
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/nombre.md` o `docs_obsoletosinvestigacion_claude/nombre.md`
- **Impacto**: FORTALECE | DEBILITA | NEUTRO
- **Resumen del impacto**: Qué dice la investigación y cómo afecta a OslaPuerto
- **Cambios en Producto.md**: Qué secciones se actualizaron y por qué

-->

## [2026-04-22] — Competidores UY
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/001_CompetidoresUY.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: Score 3.9 (#5). No competidor local en inteligencia portuaria. ANP+DNA+clima cruzados no existe.
- **Cambios en Producto.md**: Competencia

---

## [2026-04-22] — Benchmark Internacional
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/002_BenchmarkInternacional.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: project44 cobra $6250/mes + $3/container. Windward AI behavioral analytics. MarineTraffic desde $15/mes. Portcast container-centric. ANP+DNA+Uruguay XXI+clima cruzados no existe globalmente.
- **Cambios en Producto.md**: Competencia, Propuesta de Valor

---

## [2026-04-22] — Riesgos Regulatorios
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/003_RiesgosRegulatorios.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: Riesgo 1.25 (VERDE). ANP publica datos de movimientos. DNA manifiestos son públicos. Cruce de fuentes públicas es legal y defensible. Decreto 54/2017 respalda uso comercial.
- **Cambios en Producto.md**: Riesgos

---

## [2026-04-23] — Fuentes de Datos
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/004_FuentesDeDatos.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: ANP SIG público 4/5. DNA API REST 5/5. MarineTraffic API freemium 5/5. MTOP observatorio transporte 4/5. Viabilidad 4/5. Limitación: MarineTraffic histórico requiere API paga.
- **Cambios en Producto.md**: Fuentes de Datos

---

## [2026-04-24] — Sinergias Entre Verticales
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/005_SinergiasEntreVerticales.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: Cluster Trade (Customs+Company+Port+AgroExport). Cross-sell Port→Customs 60%. DNA es "Rosetta Stone" compartida. Bundle "Comercio Exterior" USD 700/mes incluye Port. Port podría ser módulo 2 de Customs.
- **Cambios en Producto.md**: Propuesta de Valor, Roadmap

---

## [2026-04-23] — Fuentes Globales Gratis y Con Permiso (Ola 001)
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/006_FuentesGlobalesGratisYConPermiso_Ola001.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: GeoNames (CC BY 4.0) para normalización de puertos y localidades portuarias. Natural Earth (dominio público) para cartografía marítima base. GLEIF para matching de navieras, operadores y agentes marítimos. Stack geográfico abierto complementa UN/LOCODE y World Port Index.
- **Cambios en Producto.md**: Fuentes de Datos

---

## [2026-04-23] — Fuentes Globales Por Vertical (Ola 003)
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/008_FuentesGlobalesPorVertical_Ola003.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: World Bank LPI para benchmark logístico por país. UN/LOCODE y World Port Index como referencia operativa de puertos. OFAC y compliance sources para screening de buques y navieras. Pero vertical de puertos sigue necesitando cierre más fino del tier legal y operativo para feeds cercanos a tiempo real.
- **Cambios en Producto.md**: Fuentes de Datos

---

## [2026-04-23] — AIS, Puertos, Terminales y Feeds de Comercio (Ola 004)
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/009_AISPuertosTerminalesFeedsComercio_Ola004.md`
- **Impacto**: FORTALECE + DEBILITA
- **Resumen del impacto**: DEBILITA: No existe feed AIS global, real-time, gratis y jurídicamente limpio. Marine Cadastre AIS (NOAA/BOEM) es solo costero/EE.UU., sin satélite, sin live feed. AISHub es intercambio contributor-based, no open data. Global Fishing Watch bajo condiciones no comerciales. Si el producto exige monitoreo global continuo, AIS cae del lado comercial. FORTALECE: SMDG Terminal Code List como child code de UN/LOCODE para terminales de contenedores. BIC Facility Codes para depots/yards (fair use, contractual). DCSA publica estándares API para Port Call, Vessel Schedules y Commercial Schedules — esqueleto operativo del dominio. La vertical no murió pero cambió de forma: combinar reference data + trade feeds + terminal codes + standards API + (si necesario) una capa comercial AIS bien elegida.
- **Cambios en Producto.md**: Fuentes de Datos, Riesgos, Arquitectura, Propuesta de Valor

---

## [2026-04-23] — Verticales Públicas UY — Ranking Final
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/019_VerticalesPublicasUYFinal.md`
- **Impacto**: NEUTRO
- **Resumen del impacto**: Port Intelligence no aparece entre las verticales top del ranking final de resiliencia a IA frontier. La dependencia de AIS comercial y la falta de feed global libre limitan su posición relativa frente a verticales con datos locales UY más fuertes (Customs, Agro, Licitaciones). Sigue siendo viable pero con moat más dependiente de capas comerciales.
- **Cambios en Producto.md**: Riesgos

---

## [2026-04-23] — Amenaza IA + Defensibilidad + Timing Comercial
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/020_AmenazaIAActualizada.md` + `docs_obsoletosinvestigacion_codex/025_DefensibilidadRealFrenteAIAAgentica.md` + `docs_obsoletosinvestigacion_codex/022_TimingYSaturacionComercial.md`
- **Impacto**: DEBILITA (como standalone)
- **Resumen del impacto**: Port Intelligence compite indirectamente con stacks enormes de logistics AI. Mejor como módulo del cluster Customs que como entrada standalone. Mercado concentrado, software logístico ya instalado, expectativa de producto alta por narrativa global de visibility/orchestration. Sin embargo, buyer y pain reales: ANP, exportadores y despachantes hablan de costos portuarios, almacenaje, demoras e impacto en producción. Sobrevive como módulo operativo del cluster comex.
- **Cambios en Producto.md**: Propuesta de Valor, Riesgos

---

## [2026-04-23] — Buyer Real y Pain Real
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/026_BuyerRealPainRealYWTP.md`
- **Impacto**: FORTALECE (como módulo)
- **Resumen del impacto**: ANP, Uruguay XXI y actores sectoriales hablan de necesidad de plataformas más eficientes, minimización de tiempos de espera de camiones, seguimiento de conectividad. Despachantes asocian atrasos a impacto directo sobre producción y quiebre de stock. Pain clarísimo y buyer también. Límite: concentración del mercado. Mejor como módulo fuerte del cluster Customs.
- **Cambios en Producto.md**: ICP, Propuesta de Valor

---

## [2026-04-23] — Fuentes AIS y Marítimas Detalladas + Tabla Referencia
- **Archivo fuente**: `docs_obsoletosinvestigacion_codex/033_FuentesDatosInternacionales.md` + `docs_obsoletosinvestigacion_codex/036_FuentesDatosUltraProfunda.md` + `docs_obsoletosinvestigacion_codex/038_TablaReferenciaFuentesDatos.md`
- **Impacto**: FORTALECE
- **Resumen del impacto**: AIS sources documentadas con más detalle: VesselFinder API (REST JSON, freemium, 500K+ vessels, real-time, score 4.8), AISHub (REST API, gratis, JSON/XML/CSV, score 4.8), aisstream.io (WebSocket, gratis, streaming global, score 4.8), MarineTraffic API (REST, freemium, port calls/ETA/vessel events, score 4.7), Data Docked (REST, freemium, 800K+ vessels, score 4.6), Datalastic (REST, freemium, score 4.6). NOTA: Ola 004 advirtió que AISHub es contributor-based y no open data reutilizable; estas fuentes listan disponibilidad técnica pero no resuelven el caveat legal para uso comercial continuo ya documentado.
- **Cambios en Producto.md**: Fuentes de Datos

## [2026-04-23] — Ranking final anti-LLM y scoring competitivo estructurado

**Archivos fuente:** `040_VerticalesPublicasUYFinal_v2.md`, `041_ResumenTotalVerticales.md`, `043_InvestigacionVerticales21x7.json`
**Impacto:** FORTALECE
**Resumen del impacto:** Port Intelligence confirma score **3.5/5** (#9) — buena vertical pero mejor como expansión del cluster comex que como punta de lanza. JSON scoring Port: buyer=4, WTP=4, saturado=2, defensa=5, ticket USD 200/mes, ciclo 60d. Competidores: Softcargo, Katoen Natie/TCP, Planir, Utilaje, Christophersen, ANP sistemas oficiales. Wedge: cruzar ANP+DNA+Uruguay XXI+clima+terminal+expediente documental para anticipar congestión, tiempos y riesgo operativo. Fleet (subvertical): buyer=5, WTP=4, saturado=3, defensa=3, ticket USD 80/mes. Competidores fleet: SGeFlota, Lógica Sur, Mekavo, Geotab/Samsara. Wedge fleet: sumar capa uruguaya (SUCIVE, SOA/BSE, inspecciones, multas) a telemetría.
**Cambios en Producto.md:** Competencia (#7), Propuesta de Valor (#4), Métricas (#10)

## [2026-04-23] — Fuentes globales gratuitas con permiso comercial

**Archivo fuente:** `042_FuentesGlobalesGratisOriginal.md`
**Impacto:** FORTALECE
**Resumen del impacto:** Fuentes Tier A para Puerto: NOAA/NCEI (CC0, bathymetry, datos costeros, clima marítimo), Copernicus Sentinel (monitoreo costero/portuario), NASA Earthdata (océanos, vientos, corrientes), ECMWF (CC BY 4.0, forecasting marítimo desde oct 2025). Nota: AISHub NO está en Tier A — sigue siendo contributor-based, no open data comercial (confirmado en Ola 004).
**Cambios en Producto.md:** Fuentes de Datos (#5)

## [2026-04-23] — Cálculos de viabilidad numérica, matriz de riesgo regulatorio y fuentes de datos profundas UY

**Archivos fuente:** `048_MatrizRiesgoRegulatorio.md`, `051_Ola4FuentesDatosProfundas.md`, `055_AnalisisNicheVsBroad_Full.md`, `056_CalculoViabilidadNumerico.md`
**Impacto:** FORTALECE
**Resumen del impacto:** Plan estratégico confirma Puerto como módulo del cluster comex, no como vertical standalone Year 1. Sin dimensionamiento numérico propio en el modelo de viabilidad. Fuentes profundas UY: ANP datos portuarios, catálogodatos.gub.uy con datasets marítimos. Nota: AIS sigue sin fuente gratuita comercial verificada.
**Cambios en Producto.md:** Roadmap (#9)

## [2026-04-25] — Resumen Total Olas 001-013 (Consolidación)

- **Archivo fuente:** `docs_obsoletosinvestigacion_codex/062_ResumenTotalOlas001a013.md`
- **Impacto:** NEUTRO
- **Resumen del impacto:** Documento de referencia que consolida las 13 olas de investigación previas en un único archivo de 95KB. No aporta información nueva sino que unifica los hallazgos ya propagados individualmente (scoring anti-LLM, fuentes de datos, competencia, viabilidad numérica, riesgo regulatorio, niche vs broad). Útil como índice maestro de toda la investigación realizada.
- **Cambios en Producto.md:** Ninguno (contenido ya propagado en batches anteriores).
