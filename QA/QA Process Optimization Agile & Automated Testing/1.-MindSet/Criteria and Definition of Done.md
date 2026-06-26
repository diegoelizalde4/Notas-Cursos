---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 1 - Mindset
tema: Criterios de aceptación y Definición de Hecho
fecha: 2026-06-17
fuente: https://www.coursera.org/learn/qa-process-optimization-agile-automated-testing/lecture/i7iOG/acceptance-criteria-and-definition-of-done
tags: [qa, agile, definition-of-done, criterios-aceptacion, epicas, historias]
---

# Criterios de aceptación y Definición de Hecho

> [!info] Idea central
> Dos herramientas responden la pregunta *"¿cuándo está terminado?"*: la **Definición de Hecho** (visión amplia, de calidad) y los **Criterios de Aceptación** (condiciones específicas por funcionalidad).

## Definición de Hecho (Definition of Done)

- Conjunto de criterios de **alto nivel** que indican cuándo un producto o incremento está **completo** y cumple la calidad esperada.
- Sirve de referencia para saber cuándo una iteración o el trabajo ha **finalizado**.

## Criterios de Aceptación (Acceptance Criteria)

- Condiciones **específicas y detalladas** que aplican a funcionalidades particulares para definir si son aceptables para el cliente.
- Actúan como un **contrato** entre el equipo Agile y los interesados, garantizando calidad y expectativas cumplidas.

## Diferencia clave

| | Definición de Hecho | Criterios de Aceptación |
|:--|:--|:--|
| **Alcance** | Amplio (incremento / versión) | Específico (una funcionalidad) |
| **Nivel** | Alto nivel, general | Detallado, concreto |
| **Función** | "¿El trabajo está terminado?" | "¿Esta función es aceptable?" |

## Estructura en Agile

```
Producto
 └─ Incremento (cada uno con su Definición de Hecho)
     ├─ Épica (característica grande)
     └─ Historia (característica pequeña) → cada una con sus Criterios de Aceptación
```

- Cada incremento tiene su propia **Definición de Hecho** que asegura calidad suficiente para avanzar.
- **Épicas** (grandes) e **historias** (pequeñas) tienen sus **criterios de aceptación** que guían el desarrollo y la validación.
- Definirlos bien es clave para la gestión de calidad: **reduce retrabajos** y **acelera la entrega**.

## Para repasar

- [ ] ¿En qué se diferencian la Definición de Hecho y los Criterios de Aceptación?
- [ ] ¿Por qué los criterios de aceptación se describen como un "contrato"?
- [ ] ¿Qué es una épica frente a una historia?

## Enlaces relacionados

- [[Integrating QA in Agile Workflows]] — QA define estos criterios en la planificación.
- [[TDD AND BDD]] — BDD escribe criterios de aceptación como escenarios *dado-cuando-entonces*.
