---
status: legacy_do_not_use_as_truth
legacy_marked_at: 2026-05-12
supersedes: C:\dev\Investigacion_Osla_consolidada\OK\modulos\osla_puerto\product.md
reason: OSLA canonical documentation moved to consolidated OK tree after V3/saneamiento audit.
do_not_use_for: product_truth, roadmap_truth, implementation_scope, claims, data_rights
---


### Críticas Ola 004-019
- **CRÍTICO:** No existe feed AIS global, real-time, gratis y jurídicamente limpio (Ola 004). Marine Cadastre es solo costero/USA. AISHub es contributor-based, no open data. Global Fishing Watch tiene condiciones no comerciales. Si producto exige monitoreo global continuo, AIS cae del lado comercial.
- **Evolución de arquitectura:** La vertical cambió de forma: combinar reference data + trade feeds + terminal codes + standards API + (si necesario) una sola capa comercial AIS bien elegida.
- **Ranking final (019):** Port Intelligence no aparece entre verticales top del ranking final. Moat más dependiente de capas comerciales que otras verticales OSLA.
# Documento de Producto: OslaPuerto

## 1. Visión del Producto

OslaPuerto es una plataforma de inteligencia portuaria que integra tracking AIS de buques, datos meteorológicos, manifiestos de carga y congestión histórica para proporcionar **predicción de ETA de embarcaciones, scheduling optimizado de atraques, y alertas tempranas de demoras**. Empodera a freight forwarders, operadores portuarios y shipping lines para tomar decisiones logísticas ágiles en tiempo real.

**Score de Viabilidad: 4.0/5**

---

## 2. Problema que Resuelve

Los freight forwarders uruguayos enfrentan fricciones críticas:
- Desconocen congestión en puertos hasta llamar al operador (pérdida de horas críticas)
- No disponen de ETA confiable de embarcaciones (dependen de fuentes no estructuradas)
- Incapacidad para optimizar scheduling de atraques (berth allocation manual)
- Forecasting de congestión basado en intuición
- Pérdida de deadlines customs/cliente por falta de visibilidad
- Riesgo de sobrecostos por demoras portuarias no anticipadas

**Consecuencias:** Impuntualidad logística, costos operacionales no predecibles, pérdida de competitividad frente a puertos de Brasil/Argentina.

**Limitación Crítica:** No existe AIS global gratuito con cobertura y precisión suficientes. Marine Cadastre (NOAA) es histórico y US-centric. Los forwarders necesitarán suscripción a AIS pagado (MarineTraffic, VesselFinder) para tracking en tiempo real.

---

## 3. Cliente Ideal (ICP)

**Primario:** Freight forwarders y agentes aduanales en Uruguay
- Volumen mínimo 500+ contenedores/año
- Cartera de clientes internacionales
- Presión por mejorar on-time delivery metrics

**Secundario:**
- Operadores portuarios (ANP, terminales privadas)
- Shipping lines (optimización de rotación de buques)
- Transportistas terrestres (coordinación última milla)

**Tamaño ICP:** ~40-60 freight forwarders activos en Uruguay con apetito tecnológico.

---

## 4. Propuesta de Valor

**Estrategia Cluster:** **Comercio Exterior** (Customs + Company + Port + AgroExport). DNA es la "Rosetta Stone" compartida entre módulos. Cross-sell Port → Customs potencial: **60%**.

| Stakeholder | Valor Entregado |
|---|---|
| **Freight Forwarders** | ETA prediction con MAPE <0.5% (vs. margen de error actual ±12h). Dashboard unificado (AIS + weather + carga). Alertas proactivas de demora 48-72h. Reducción de reclamos cliente por impuntualidad. |
| **Operadores Portuarios** | Optimización de berth scheduling (MIP solver). Predicción de congestión 7 días. Mejora de utilización de infraestructura. |
| **Shipping Lines** | Visibilidad de rotación de buques. Optimización de viajes (timing de entrada a puerto). |

**Precio:** USD 300-500/mes (por usuario/empresa; tier de features según volumen de carga)

**Bundle "Comercio Exterior":** USD 700/mes (incluye Port como módulo dentro de plataforma Customs). **Recomendación:** Puerto podría posicionarse como "Módulo 2" de Customs en lugar de producto standalone.



**Posicionamiento Estratégico (Ola 004-019):**

Puerto Intelligence rankea **mejor como módulo del cluster Customs** que como producto standalone Year 1:
- **Buyer y pain reales:** costos portuarios, almacenaje, demoras, quiebre de stock
- **Cross-sell Port → Customs:** potencial 60%
- **Recomendación:** Puerto como "Módulo 2" de plataforma Customs (no producto independiente)
- **Timing:** Post-MVP Customs (Q2–Q3 2026), integración nativa como feature comex

**Limitación Crítica de Datos (Ola 004-019):**
AIS gratuito de calidad NO existe a escala global. Marine Cadastre es históricamente limitado (US waters), retrasado (2-4 sem), cobertura incompleta Atlántico Sur. MVP debe incorporar feed AIS pagado (MarineTraffic/VesselFinder) desde marcha: USD 500–1.500/mes adicional presupuesto. AISHub listado como gratis pero es contributor-based (no open data reutilizable comercial).
---


**Ola 004: Redefinición de Port Intelligence**
La Ola 004 redefine Port Intelligence: ya no basta 'encontrar una fuente gratis'. Lo inteligente es combinar reference data abierta, trade feeds limpios, terminal/facility code lists, standards API abiertos y, si se necesita monitoreo global continuo, una sola capa comercial AIS bien elegida.
## 5. Fuentes de Datos

### Fuentes Uruguayas (Acceso Directo/Contacto)
- **ANP (Administración Nacional de Puertos):** Cronogramas de atraques, datos de navíos historicales, congestión portuaria. **Score 4/5** - SIG público, datos movimientos de buques publicados
- **DNA (Dirección Nacional de Aduanas):** Manifiestos de importación/exportación, horarios de despacho. **Score 5/5** - API REST disponible, manifiestos públicos
- **BCU (Banco Central del Uruguay):** Tasas de cambio, índices de comercio
- **IMPO (Instituto Mexicano de Propiedad Industrial):** Datos de certificación de carga (si aplica)
- **MTOP (Ministerio de Transporte y Obras Públicas):** Observatorio de datos portuarios. **Score 4/5**

### Fuentes Internacionales (Acceso Pagado/Historico)
- **Marine Cadastre AIS (NOAA):** Histórico AIS 2009-presente para región Atlántico Sur (acceso libre pero retrasado/limitado)
- **MarineTraffic:** AIS en tiempo real global. **Score 5/5** - API freemium desde USD 15/mes (freemium level), cobertura global. Limitación: histórico requiere API paga
- **VesselFinder:** AIS en tiempo real global (alternativa a MarineTraffic)
- **NOAA Tides & Currents:** Predicción de mareas, corrientes (CC0)
- **ECMWF ERA5 + Forecast:** Datos climáticos históricos + predicción 7-15 días (CC BY 4.0)
- **UN/LOCODE:** Código de puertos internacionales
- **World Port Index:** Características de puertos globales

**Viabilidad de Fuentes: 4/5**. Limitación crítica: MarineTraffic histórico requiere suscripción paga. La combinación ANP + DNA + MarineTraffic es defensible y no existe globalmente.


### Nuevas Fuentes Internacionales (Ola 004-019) — Estándares y Reference Data

| Fuente | Tipo | Cobertura | Viabilidad |
|--------|------|-----------|-----------|
| **GeoNames** | Reference data | Normalización puertos y localidades | 5/5 |
| **Natural Earth** | Cartografía | Datos marítimos dominio público | 5/5 |
| **GLEIF** | Corporate | Matching navieras, operadores, agentes marítimos | 5/5 |
| **SMDG Terminal Codes** | Estándares | Child codes UN/LOCODE para terminales contenedores | 5/5 |
| **BIC Facility Codes** | Estándares | Depots, yards, instalaciones container-side | 4/5 |
| **DCSA (Digital Container Shipping Association)** | API Abierto | Port Call, Vessel Schedules, Commercial Schedules; estándar industria | 5/5 |

**Viabilidad agregada: 4.8/5** (vs. anterior 4/5 sin DCSA)

---

### Arquitectura Recomendada (Ola 004) — DCSA como Esqueleto Operativo

DCSA aporta esqueleto operativo compartido:
- **Eventos:** Port Call, Cargo Ready, Container Load/Discharge
- **Timestamps:** Estándar cronológico entre carriers, terminals, partners
- **Objetos:** Vessel, Container, Booking, Shipment, Party
- **Interacciones:** Por quién, cuándo, qué evento

**Beneficio:** Reduce fricción de interoperabilidad incluso si data concreta viene de fuentes privadas (MarineTraffic, ANP).

**Núcleo recomendado:**
1. UN/LOCODE (nodo macro puerto)
2. SMDG Terminal Codes (nodo terminal específico)
3. BIC Facility Codes (yards, depots)
4. DCSA eventos (capa operativa integrada)

Permite MVP con **reference data abierta + trade feeds limpios + AIS pagado** sin fragmentación.


### Limitación Crítica de Datos
**AIS gratuito de calidad no existe a escala global.** Marine Cadastre es:
- Históricamente limitado (principalmente US waters)
- Retrasado (datos con lag de 2-4 semanas)
- Cobertura incompleta en Atlántico Sur

**Solución:** MVP debe incorporar feed AIS pagado desde marcha (MarineTraffic/VesselFinder). Presupuesto adicional ~USD 500-1500/mes por data.

---


### Nuevas Fuentes Internacionales (Ola 004-019)
- **GeoNames** (CC BY 4.0): normalización de puertos y localidades
- **Natural Earth** (dominio público): cartografía marítima base
- **GLEIF:** matching navieras, operadores, agentes marítimos
- **SMDG Terminal Code List:** child codes de UN/LOCODE para terminales de contenedores
- **BIC Facility Codes:** depots, yards, instalaciones container-side (fair use, contractual)
- **DCSA:** estándares API para Port Call, Vessel Schedules, Commercial Schedules
- **Marine Cadastre AIS** (NOAA/BOEM): AIS histórico costero USA (sin live feed, sin satélite)
## 6. Modelos ML Defensibles

### 6.1 Vessel ETA Prediction (XGBoost)
- **Input:** Historial de viajes (timestamps entrada/salida), características del buque (tipo, eslora, calado), puerto origen/destino, condiciones climáticas ECMWF, carga (contenedores, graneles)
- **Output:** ETA predicha + intervalo de confianza (±2-6 horas)
- **Métrica:** MAPE <0.5% (error medio 1-2 horas en travesías 5-15 días)
- **Ventaja defensible:** Histórico de atraques ANP + datos AIS => modelos específicos a ruta UY; cambios de horario ante clima no capturados por modelos genéricos

### 6.2 Berth Scheduling (Mixed Integer Programming)
- **Input:** ETAs predichas, tipo de carga, requerimientos de berth, duración estimada descarga (histórica)
- **Output:** Asignación óptima berth + horario de atraque para minimizar tiempo de espera
- **Métrica:** Reducción de espera promedio 20-30%; utilización berth +15%
- **Ventaja defensible:** Modelo específico a puertos UY; constraint knowledge ANP

### 6.3 Congestion Forecasting (LSTM)
- **Input:** Series temporal de llegadas de buques (7 días anteriores), tipo de carga, berth utilización histórica
- **Output:** Predicción de índice de congestión (0-100%) para próximos 7 días
- **Métrica:** RMSE <15 puntos de congestión; AUROC >0.80 para alerta congestión moderada
- **Ventaja defensible:** Datos ANP de congestión histórica; generalización a patrones estacionales

### 6.4 Weather Risk Integration
- **Input:** Forecast ECMWF (viento, olas, precipitación) + histórico de cancelaciones
- **Output:** Probabilidad de demora/cancelación por clima en próximas 72h
- **Métrica:** AUROC >0.85 para eventos de demora severa
- **Ventaja defensible:** Entrenado con histórico de demoras reales ANP; regional

---

## 7. Competencia y Diferenciación

**Score Competitivo: 3.5/5 (#9 en Ranking Final)**

### Competidores por Componente

#### Software de Despacho y Terminal
- **Softcargo**: Software despacho genérico
- **Katoen Natie / TCP**: Operadores terminales; software proprietary
- **Planir, Utilaje, Christophersen**: Soluciones especializadas; sin ETA prediction
- **ANP sistemas oficiales**: Cronogramas; sin predicción

#### Fleet Tracking y Telemetría
- **SGeFlota, Lógica Sur, Mekavo**: Flota terrestre; sin integración marítima
- **Geotab / Samsara** (global): IoT genérico; sin contexto portuario Uruguay
- **UTE sistema de flota**: Estatal; sin publicación abierta

### Amenaza IA Frontier

**Logistics AI Globales** (project44, FourKites, Descartes) ya empujan visibility/orchestration. project44 +48% new ARR, FourKites/Descartes USD 729M revenue. Oportunidad solo como **módulo local complementario**, no como competidor directo.

### Diferenciación Defensible

| Aspecto | OslaPuerto | Competidores |
|--------|-----------|--------------|
| **Integración ANP + AIS + Clima** | Stack único local | No existe globalmente |
| **ETA Prediction ultra-precisa** | MAPE <0.5% | Industria ±12h |
| **Berth Scheduling automático** | MIP solver | Manual en región |
| **Forecasting congestión 7d** | LSTM local | Ad-hoc |
| **Defensa contra LLMs** | Datos ANP estructurados | Replicable con scraping |

### Riesgos Críticos de Datos

**AIS gratuito de calidad NO existe a escala global.** Marine Cadastre es:
- Históricamente limitado (principalmente US waters)
- Retrasado (datos con lag 2-4 semanas)
- Cobertura incompleta Atlántico Sur

**MVP debe incorporar feed AIS pagado** (MarineTraffic/VesselFinder desde marcha). Presupuesto ~USD 500-1500/mes adicional.

**NOTA LEGAL CRÍTICA**: AISHub es contributor-based (NO open data comercial reutilizable). Disponibilidad técnica ≠ permiso legal.

### Arquitectura Recomendada (Ola 004)

DCSA como esqueleto operativo: eventos, timestamps, objetos e interacciones. Reduce fricción interoperabilidad incluso con data privada. Núcleo: UN/LOCODE (nodo macro) + SMDG (terminal) + BIC (facility) + DCSA (esquema operativo).

### Métricas de Mercado

| Métrica | Buyer | WTP | Saturado | Defensa | Ticket | Ciclo |
|---------|-------|-----|----------|---------|--------|-------|
| **Port** | 4/5 | 4/5 | 2/5 | 5/5 | USD 200/mes | 60d |
| **Fleet** | 5/5 | 4/5 | 3/5 | 3/5 | USD 80/mes | 30d |

### Recomendación Estratégica

Port Intelligence mejor como **módulo del cluster Customs** que standalone. Buyer y pain reales: costos portuarios, almacenaje, demoras, quiebre de stock. ANP, Uruguay XXI y actores hablan de plataformas más eficientes. Límite: concentración mercado + competencia indirecta con stacks enormes logistics AI.



## 8. Arquitectura Técnica

### Stack Principal
- **Backend:** FastAPI + Gunicorn + Nginx
- **Base de Datos:** PostgreSQL 16 + PostGIS (queries espaciales AIS)
- **Cache/Queue:** Redis (datos AIS cachés, cola de cálculos)
- **ML - ETA Prediction:** XGBoost + LightGBM + scikit-learn
- **ML - Congestión:** PyTorch LSTM + Keras
- **Optimización:** OR-Tools (berth scheduling MIP)
- **Frontend:** Next.js 15 + Mapbox (visualización AIS en tiempo real)
- **Orquestación:** Airflow (DAG: descarga AIS → cálculo ETA → scheduling)
- **Mensajería:** Kafka (fase 4 para stream AIS en tiempo real)
- **Monitoreo:** Prometheus + Grafana


### Estándares Operativos (DCSA v2.2+)

OslaPuerto adopta Digital Container Shipping Association (DCSA) como esqueleto operativo:
- **Port Call Events:** Vessel arrival, berth allocation, cargo operations, departure
- **Vessel Schedules:** Planned vs. actual ETAs, delays, port sequencing
- **Commercial Schedules:** Booking to delivery, integrated shipment tracking
- **Party/Role Management:** Carrier, Terminal, Freight Forwarder, Customs Broker, Trucker

**Beneficio:** Interoperabilidad nativa con sistemas carriers (Maersk, MSC) y terminals. Reduce mapping efforts, soporta integración post-MVP con plataformas logísticas (Descartes, Blue Yonder).



### Fuentes de Datos (Integración)
- **AIS Pagado:** API MarineTraffic/VesselFinder (tiempo real)
- **ECMWF API:** Forecast meteorológico cada 6 horas
- **ANP API (contacto directo):** Cronogramas atraques, carga descargada
- **Scrapers custom:** DNA (manifiestos aduanales si no disponible API)

### Flujo de Datos (Alto Nivel)
1. Feed AIS pagado ingresa a Kafka / endpoint HTTP (buques en ruta a UY)
2. Validación y enriquecimiento con datos ANP (buque ya visto en región)
3. Ejecución ETA Prediction (XGBoost) con ECMWF, historial viajes
4. Cálculo de Berth Scheduling (OR-Tools MIP)
5. Forecast Congestión (LSTM) basado en llegadas predichas
6. Dashboard time-series: posición AIS + ETA + risk score
7. Alertas threshold-based: demora esperada >12h, congestión >80%
8. API REST para integración con sistemas TMS (Transportation Management System)

### Escalabilidad
- Redis para cachés AIS de buques (TTL 1 hora)
- PostgreSQL + índices GiST para queries espaciales rapidas
- OR-Tools puede resolver MIP para 20-50 atraques en <1s
- Kafka para escalabilidad a fase 4 (streaming en tiempo real)

---

## 9. Roadmap Resumido

### Fase 1 (Meses 1-2): MVP - ETA Prediction
- Integración AIS pagado (MarineTraffic o VesselFinder)
- Integración ECMWF forecast
- Modelo ETA XGBoost (MAPE <0.5%)

### DCSA como Esqueleto Operativo (Ola 004)
DCSA aporta esqueleto operativo: eventos, timestamps, objetos e interacciones entre carriers, terminals y partners. Reduce fricción de interoperabilidad incluso si la data concreta viene de fuentes privadas. Arquitectura recomendada: UN/LOCODE (nodo macro) + SMDG (terminal) + BIC (facility) + DCSA (esquema operativo).
- Dashboard básico (mapa de buques, ETA, timeline)
- API REST para acceso a ETAs
- Piloto con 2-3 freight forwarders

### Fase 2 (Meses 3-4): Congestión + Scheduling
- Forecast congestión LSTM
- Berth Scheduling automático (OR-Tools MIP)
- Alertas Whatsapp/email proactivas
- Reportes diarios congestión
- Integración ANP data API (si disponible)

### Fase 3 (Meses 5-6): Integración + B2B
- API con estándares logísticos (EDI, JSON)
- Integración TMS común (SAP, Descartes, Blue Yonder)
- Admin panel: usuarios, cuotas, reportes de uso
- Mobile app (iOS/Android) para forwarders
- SLA 99.5% uptime

### Fase 4 (Post-MVP): Avances
- Streaming AIS con Kafka (latencia <10seg)
- Modelos predictivos por tipo de carga (contenedores, graneles, autos)
- Integración radar meteorológico (RMA)
- Expansion a puertos Argentina/Brasil
- Marketplace de datos históricos (anonimizados)

---

## 10. Métricas de Éxito

| Métrica | Target | Timeline |
|---|---|---|
| **MAPE ETA Prediction** | <0.5% en validación | Mes 2 |
| **Cobertura Buques** | 100% grandes buques (>500 TEU) a UY | Mes 2 |
| **RMSE Congestión Forecast** | <15 puntos (0-100 escala) | Mes 4 |
| **Utilización Berth** | +15% vs. baseline | Mes 4 |
| **Clientes Pagando** | 3-5 freight forwarders | Mes 6 |
| **MRR Objetivo** | USD 1.5K-2.5K | Mes 6 |
| **Uptime API** | 99.5% | Mes 6 |
| **Latencia ETA Calc** | <30seg para nuevo buque | Mes 4 |
| **NPS Usuarios Piloto** | >50 | Mes 6 |

---

## 11. Riesgos y Mitigaciones

**Riesgo Overall: 1.25/5 (GREEN)** ✓

La arquitectura legal es defensible:
- ANP publica datos de movimiento de buques

### Reformulación del Producto (Investigaciones 020-026)
Reformulación (020-026): Port Intelligence mejor como módulo del cluster Customs que como producto standalone. Buyer y pain reales: costos portuarios, almacenaje, demoras, quiebre de stock. ANP, Uruguay XXI y actores hablan de plataformas más eficientes. Límite: concentración del mercado y competencia indirecta con stacks enormes de logistics AI.

### Riesgos de Posicionamiento Estratégico (Investigaciones 020-031)
- Port compite indirectamente con stacks globales (project44, FourKites, Descartes). No conviene como primera bandera — mercado concentrado, software logístico ya instalado, expectativa alta.
- Mejor entrada: expansión natural del cluster comex después de Customs. No standalone.

### Logistics AI Globales (Investigaciones 020-026)
Logistics AI globales ya empujan visibility/orchestration con mucha fuerza. project44 cash flow positivo, +48% new ARR. FourKites y Descartes (USD 729M revenue FY2026). Oportunidad solo como módulo local complementario, no como competidor directo.

### AIS APIs Documentadas (Investigaciones 033+036+038)

VesselFinder API (REST JSON, freemium, 500K+ vessels, score 4.8), aisstream.io (WebSocket, gratis, streaming global, score 4.8), MarineTraffic API (REST, freemium, port calls/ETA, score 4.7), Data Docked (REST, freemium, 800K+ vessels, score 4.6), Datalastic (REST, freemium, score 4.6).


### Riesgo 3: Ranking final (019) y posicionamiento estratégico

**Descripción**: Port Intelligence NO aparece entre verticales top del ranking final (019). Moat más dependiente de capas comerciales (AIS pagado) que otras verticales OSLA. Riesgo de recursos dispersos en producto poco defendible vs. LLMs + compresión competitiva con stacks globales.

**Probabilidad**: Alta  
**Impacto**: Alto (afecta priorización estratégica)

**Contexto (Ola 004-019)**:
- **Ranking final (019):** Puerto Intelligence fuera de top 10; Real Estate Intelligence es precursor débil (2/5 defensibilidad)
- **Compresión competitiva global:** project44 (+48% ARR), FourKites, Descartes (USD 729M revenue)
- **Amenaza LLM:** Gemini + datos públicos = 80% due diligence logística replicable rápidamente
- **AIS crítico:** No existe gratis/abierto a escala global; MarineTraffic/VesselFinder USD 500–1.500/mes mandatory

**Mitigaciones** (refuerzan estrategia Customs cluster):
- **NO lanzo Puerto standalone Year 1.** Ingresa como Módulo 2 de Customs post-MVP (Q2–Q3 2026)
- **Buyer real:** Forwarders resuelven problema combinado: arancel + congestión + demora (no puerto aislado)
- **Cross-sell dinámico:** DNA (aduanas) → puerto cost reduction → shared customer
- **Viabilidad mejorada:** Pilotos con 2–3 freight forwarders de Customs cluster (no standalone)

---

### Riesgo 4: AIS Gratuito Vs. Legal (Ola 004-019 Crítico)

**Descripción**: Disponibilidad técnica de AIS ≠ permiso legal para uso comercial. AISHub "gratis" es contributor-based (NO open data reutilizable). Riesgo de breach de ToS si MVP sobre AISHub sin comprobación legal.

**Probabilidad**: Media  
**Impacto**: Alto (reputación, legal)

**Contexto**:
- **Marine Cadastre (NOAA):** Histórico, retrasado (2-4 sem lag), US waters
- **AISHub:** Gratis pero contributor-based, ToS ambigua re: comercial
- **MarineTraffic:** API freemium desde USD 15/mes, histórico requiere API paga (USD 500+/mes)
- **VesselFinder:** Alternativa a MarineTraffic, similar pricing
- **aisstream.io:** WebSocket gratis, streaming global, score 4.8 (verificar ToS)

**Mitigaciones (CRÍTICAS)**:
- **MVP debe incorporar AIS pagado DESDE MARCHA.** No confiable usar "freemium" como base
- Presupuesto dedicado: USD 500–1.500/mes AIS (incluir en modelo costos)
- Verificación legal exhaustiva de ToS antes de integración (especialista legal)
- Opciones paralelas: MarineTraffic (4.7), VesselFinder (4.7), aisstream.io (4.8, verificar) en order de preferencia

---

### Riesgo 5: Redefinición de Product-Market Fit Post-Ola 004

**Descripción**: Ola 004 redefine Port Intelligence: ya no basta "encontrar una fuente gratis". Lo inteligente es combinar reference data abierta + trade feeds limpios + estándares (DCSA, UN/LOCODE) + AIS pagado bien elegido.

**Probabilidad**: Certeza  
**Impacto**: Medio-Alto (refuerza arquitectura pero requiere rebalance)

**Implicaciones**:
- **DCSA como esqueleto:** Reduce fricción interoperabilidad; estándar industria (adoptado Maersk, MSC, CMA CGM)
- **No es producto autónomo:** Es "enabler" de Customs → Port → Fleet integración
- **Roadmap revisado:** Phase 1 MVP cae a soporte Customs (Q3 2026), no independencia
- **Go-to-market:** Cluster Customs + Port, no Port standalone (evita competencia frontal Descartes)

**Mitigaciones**:
- Adoptar DCSA explícitamente en arquitectura (sección 8.1 actualizada)
- Replanificar roadmap con Port como Módulo 2 (no Phase 4)
- Alinear roadmap Customs y Port (dependencies)
- Comunicar repositioning claro al equipo (evita sorpresas recursos)


**NOTA LEGAL CRÍTICA:** AISHub listado como gratis (score 4.8) pero Ola 004 advirtió que es contributor-based, no open data reutilizable para uso comercial continuo. Disponibilidad técnica ≠ permiso legal.
