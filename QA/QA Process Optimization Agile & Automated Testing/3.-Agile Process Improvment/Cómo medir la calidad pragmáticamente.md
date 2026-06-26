---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 3 - Mejora del Proceso Agile
tema: Cómo medir la calidad pragmáticamente (lectura)
fecha: 2026-06-26
tipo: artículo de lectura
tags: [qa, calidad, iso-9000, bdd, eficacia, eficiencia, velocity]
---

# Cómo medir la calidad pragmáticamente

> [!info] Idea central
> La calidad no debe medirse contando bugs ni con juicios subjetivos. Se mide evaluando **cuánto alcance se entregó**, **qué tanto logró los objetivos de negocio** y **si el proceso fue eficiente**.

## ¿Qué es la calidad?

Definición ISO 9000:
> *"La calidad es el grado en que un conjunto de características inherentes de un objeto cumple con los requisitos."*

Aplicada al software, se divide en **tres dimensiones**:

| Dimensión | Pregunta que responde |
|:--|:--|
| **Calidad técnica** | ¿Cumple los requisitos funcionales y no funcionales (las especificaciones)? |
| **Calidad de negocio** | ¿Resuelve el problema del negocio y entrega el valor esperado? |
| **Calidad del proceso (eficiencia)** | ¿Se usaron bien los recursos: a tiempo y dentro del presupuesto? |

## El error de usar los "bugs" como métrica

- Encontrar y documentar errores es vital para la mejora continua, **pero contar bugs es irrelevante** para medir la calidad real.
- Menos errores **no** significa automáticamente más calidad, sobre todo si el software no entrega valor.
- KPIs basados en nº de bugs ("errores por mil líneas") **se desaconsejan**: desvían el foco de la entrega de valor.

## Cómo medir cada dimensión

### 1. Calidad técnica (eficacia del alcance)
- Definir el alcance con **escenarios precisos** (se recomienda **BDD**).
- Métrica: **% de escenarios funcionales entregados con éxito**.
  > Ej.: 50 escenarios planeados, 45 funcionan en producción → **90 %** de calidad técnica.

### 2. Calidad de negocio (eficacia de objetivos)
- Desglosar grandes objetivos ("aumentar ventas") en métricas pequeñas y **atribuibles al software** ("tasa de conversión", "tamaño promedio del pedido").
- Definirlas **al inicio**: a menudo el software debe construirse de cierta forma para poder recolectar esos datos.

### 3. Calidad del proceso (eficiencia)
- Mide qué tan bien ejecuta el equipo frente al **plan original**.
- Si el equipo **estima de forma confiable y cumple** sus estimaciones, el negocio puede invertir con seguridad.
- No poder comprometerse con estimaciones indica ineficiencias → se mide con **Velocity** o **burn-down charts**.

## Conclusión

> [!tip] Para recordar
> La calidad ni es subjetiva ni se mide con métricas vacías como el conteo de bugs. Es: **cuánto del alcance esperado se entregó**, **qué tan bien logra los resultados de negocio**, y **si el proceso fue eficiente y controlado**.

## Para repasar

- [ ] Enuncia la definición de calidad de ISO 9000.
- [ ] ¿Por qué el conteo de bugs es una mala métrica?
- [ ] ¿Cómo se mide la calidad técnica con BDD? Da un ejemplo con porcentaje.
- [ ] ¿Con qué métricas ágiles se mide la eficiencia del proceso?

## Enlaces relacionados

- [[Métricas y KPIs para QA Agile]] — la versión "catálogo" de estas mismas ideas.
- [[TDD AND BDD]] — el enfoque BDD que se recomienda para definir el alcance.
- [[Optimización continua de QA]] — cómo seguir mejorando con estas métricas.
