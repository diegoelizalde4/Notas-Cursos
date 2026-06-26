---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 2 - Estrategias de Testing Agile
tema: Gestión de escenarios de prueba Agile
fecha: 2026-06-23
fuente: https://www.coursera.org/learn/qa-process-optimization-agile-automated-testing/lecture/z4BiH/agile-test-scenarios-management
tags: [qa, test-suites, automatizacion, exploratorias, sesiones-prueba]
---

# Gestión de escenarios de prueba Agile

> [!info] Idea central
> Las pruebas se organizan en **test suites** (colecciones de casos). Hay que decidir **qué automatizar** y **qué probar manualmente**, y combinar sesiones **scriptadas** con **exploratorias**.

## ¿Qué es un test suite?

Conjunto de casos de prueba **agrupados** para evaluar una característica, módulo o toda la aplicación. Un mismo escenario puede pertenecer a **varias suites** (reutilización).

## Tipos de test suites

| Suite | Propósito |
|:--|:--|
| **Sprint** | Pruebas para cerrar el trabajo del sprint y alimentar la *sprint review*. |
| **Regresión** | Se ejecuta al añadir nueva funcionalidad; **acumula** pruebas de sprints anteriores. |
| **Smoke** | Variante de regresión: verifica **funciones críticas** de forma rápida. |
| **Producción (prod)** | Diseñada para **no interferir** con el negocio (sin alertar a clientes reales ni afectar reportes). |
| **Módulo** | Se enfoca en probar **módulos individuales** de la solución. |

> [!note] Nota
> Las **pruebas unitarias** normalmente **no** se incluyen en estas suites: se ejecutan automáticamente durante el desarrollo y el despliegue.

## ¿Cuándo automatizar un caso?

> [!check] Automatiza cuando…
> - Se **repite con frecuencia** (misma función en cada cambio).
> - Toma **mucho tiempo** manualmente (varios navegadores o dispositivos).
> - Tiene resultados **determinísticos** (aprobado/fallado, sin interpretación humana).
> - La funcionalidad es **estable** (no cambia mucho → la automatización no se vuelve obsoleta).
> - Involucra **grandes volúmenes de datos** o pruebas **sin interfaz gráfica** (BD, APIs).

> [!x] Prefiere pruebas manuales cuando…
> - Se requiere **juicio humano**.
> - La **interfaz cambia** con frecuencia.
> - La funcionalidad es **temporal**.
> - Se necesita una prueba **rápida y puntual**.

## Sesiones de prueba

Periodo de tiempo definido para ejecutar y analizar pruebas con un objetivo claro:

- **Scriptada:** con pruebas definidas y a menudo automatizadas.
- **Exploratoria:** sin guion, enfocada en **descubrir defectos** y oportunidades de mejora.

## Buenas prácticas

- Gestionar **activamente** los test suites y definir casos de uso claros para cada uno.
- Evaluar el **valor de automatizar** frente al esfuerzo requerido (es una inversión).
- **Combinar** pruebas automatizadas y exploratorias para cubrir escenarios previstos **y** casos límite.

## Para repasar

- [ ] Diferencia entre suite de regresión y smoke suite.
- [ ] Da tres criterios para decidir automatizar un caso.
- [ ] ¿Qué busca una sesión exploratoria que una scriptada no?
- [ ] ¿Por qué las unitarias no van en estas suites?

## Enlaces relacionados

- [[Foundations of test Automation]] — los tipos de prueba que componen las suites.
- [[TDD AND BDD]] — origen de las pruebas automatizadas.
- [[Optimización continua de QA]] — priorizar pruebas por riesgo e impacto.
