---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 3 - Mejora del Proceso Agile
tema: Métricas y KPIs para QA Agile
fecha: 2026-06-24
fuente: https://www.coursera.org/learn/qa-process-optimization-agile-automated-testing/lecture/5duzG/metrics-and-kpis-for-agile-qa
tags: [qa, metricas, kpi, mttd, mttr, defect-leakage, csat]
---

# Métricas y KPIs para QA Agile

> [!info] Idea central
> Sin métricas no se sabe si QA realmente mejora la calidad. La gran lección: **dejar de contar bugs y empezar a medir el valor entregado**. La métrica técnica que más importa es la **fuga de defectos**.

## ¿Por qué medir?

- Sin métricas es difícil saber si QA **mejora la calidad** o solo cumple tareas superficiales.
- Permiten **identificar riesgos** antes de que se vuelvan fallos y **demostrar el valor** del proceso de QA.

## Las tres categorías de métricas

### 1. Calidad técnica
Mide qué tan bien el producto cumple los requisitos funcionales y no funcionales.

| Métrica | Qué mide |
|:--|:--|
| **Fuga de defectos** *(Defect Leakage)* | Errores que **escapan a producción** y llegan al usuario. ⭐ La más importante. |
| **Densidad de defectos** *(Defect Density)* | Nº de defectos por unidad de tamaño (p. ej. por mil líneas de código). |
| **Distribución de severidad** | Proporción de defectos graves frente a menores. |
| **Cobertura de pruebas** *(Test Coverage)* | % de componentes/código/requisitos cubiertos por pruebas. |

> [!warning] Cuidado
> **Contar bugs antes del lanzamiento NO es buena métrica de calidad.** Lo que importa es el valor entregado, no cuántos errores se registraron internamente.

### 2. Calidad de negocio
Mide hasta qué punto el producto logra los objetivos de la empresa.

| Métrica | Qué mide |
|:--|:--|
| **KPIs comerciales** *(Business KPIs)* | Logro de un objetivo de negocio (p. ej. si la meta es vender más → tasa de conversión en el checkout). |
| **CSAT** | Satisfacción del cliente. Indicador de "último recurso": si **cae** tras lanzar algo, la calidad de negocio falla. |

### 3. Calidad del proceso de QA
Mide la eficiencia y eficacia del propio proceso de pruebas.

| Métrica | Qué mide |
|:--|:--|
| **Confiabilidad de la prueba** *(Test Reliability)* | Proporción de **falsos positivos**. A menos, más confiable. |
| **MTTD** *(Mean Time to Detect)* | Tiempo medio desde que se **introduce** un defecto hasta que se **descubre**. |
| **MTTR** *(Mean Time to Repair)* | Tiempo medio en **resolver y revalidar** un defecto ya descubierto. |
| **Wait time to start testing** | Tiempo que una función desarrollada **espera** para ser probada (mide desconexión del flujo). |
| **Velocidad de ejecución** *(Test execution speed)* | Tiempo en completar la suite de pruebas. |

## MTTD vs MTTR

| | MTTD | MTTR |
|:--|:--|:--|
| **Mide** | Velocidad para **encontrar** el problema | Velocidad para **solucionarlo y verificarlo** |
| **Desde → hasta** | Introducción → detección | Detección → resolución validada |
| **Objetivo** | Más corto = ciclo de feedback más rápido | Más corto = mejor, **pero** ojo: reparar bugs de baja prioridad tarde puede distorsionar el promedio |

## Ajustes proactivos (métricas de proceso)

| Métrica | Valor alarmante | Recomendación |
|:--|:--|:--|
| **Cobertura de pruebas** | Demasiado baja | Automatizar, añadir recursos, distribuir responsabilidad, añadir un *gate check*. |
| **Confiabilidad de la prueba** | Demasiado baja | Ajustar pruebas automatizadas, introducir *three amigos*, capacitar en el negocio. |
| **MTTD** | Demasiado alto | Reajustar suites, cambiar frecuencia, aumentar cobertura, usar exploratorias. |
| **MTTR** | Demasiado alto | Mejorar priorización/triaje, sesiones de re-verificación, automatizar *rollbacks*. |
| **Wait time to start testing** | Demasiado alto | Revisar el flujo end-to-end, introducir sistema *pull*, reevaluar recursos. |
| **Tiempo de ciclo de pruebas** | Demasiado alto | Más automatización, pruebas en paralelo, revisar cuellos de botella, integrar con CI/CD. |

## Ajustes reactivos (métricas técnicas y de negocio)

| Métrica | Valor alarmante | Recomendación |
|:--|:--|:--|
| **Fuga de defectos** | Demasiado alta | Aumentar cobertura, capacitar testers, automatizar, exploratorias, mejorar regresión, nuevos *gates* (UAT, BVT). |
| **Densidad de defectos** | Demasiado alta | Refactorizar áreas complejas, mejorar estándares, validación más estricta antes de fusionar. |
| **Distribución de severidad** | Muchos defectos graves | Priorizar QA en lo crítico, *gates* más estrictos, optimizar diseño de pruebas. |
| **KPIs comerciales** | Fuera de objetivo | Realinear alcance con objetivos, involucrar SMEs/consultores, entrevistar clientes. |
| **CSAT** | En declive | Encuestar/entrevistar clientes, recopilar feedback. |

## Conclusión: contar bugs → medir valor

> [!tip] Tres ideas para memorizar
> 1. **Contar errores antes del lanzamiento es irrelevante:** si el software se lanza y entrega valor, el equipo hizo un buen trabajo sin importar cuántos bugs registró.
> 2. **El foco real es la Fuga de Defectos:** lo que escapa a producción. La meta ideal → **cero**.
> 3. **La técnica no sirve si el negocio falla:** el indicador definitivo es **CSAT**. Si cae al lanzar funciones, no se cumple el objetivo de calidad.

## Para repasar

- [ ] ¿Por qué contar bugs no mide la calidad?
- [ ] Diferencia exacta entre MTTD y MTTR.
- [ ] ¿Cuál es la métrica técnica más importante y cuál su meta ideal?
- [ ] ¿Qué harías si la cobertura de pruebas es demasiado baja? ¿Y si MTTR es muy alto?
- [ ] ¿Por qué CSAT es el indicador de "último recurso"?

## Enlaces relacionados

- [[Cómo medir la calidad pragmáticamente]] — el artículo que profundiza esta misma idea.
- [[Foundations of test Automation]] — cómo subir la cobertura.
- [[Optimización continua de QA]] — indicadores líderes vs rezagados.
