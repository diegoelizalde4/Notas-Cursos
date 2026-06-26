---
curso: Introduction to DevOps
modulo: Visión General de DevOps
tema: XP, Agile y el origen de DevOps
fecha: 2026-06-24
fuente: https://www.coursera.org/learn/intro-to-devops/lecture/F4riZ/xp-agile-and-beyond
tags: [devops, agile, xp, extreme-programming, manifiesto-agile, shadow-it]
---

# XP, Agile y más allá

> [!info] Idea central
> **Extreme Programming (XP)** inició el movimiento **Agile**, que mejoró el desarrollo pero **no resolvió el lado de Operaciones**. Esa brecha ("IT de dos velocidades") es lo que **DevOps** viene a cerrar.

## Línea de tiempo

| Año | Hito | Quién |
|:--|:--|:--|
| 1996 | Nace **Extreme Programming (XP)** | Kent Beck |
| 2001 | Se firma el **Manifiesto Agile** | 17 desarrolladores |
| Después | Surge **DevOps** para integrar Agile con Operaciones | Comunidad |

## Extreme Programming (XP)

- Metodología creada por **Kent Beck en 1996**.
- Se basa en un enfoque **iterativo con ciclos de retroalimentación muy cortos** para mejorar la calidad y responder rápido a cambios del cliente.
- Incluye prácticas como la **programación en pareja (pair programming)**: dos desarrolladores trabajan juntos en el mismo código para mejorar la calidad y compartir conocimiento.

## El Manifiesto Agile (2001)

Agile formalizó las metodologías ligeras como XP. Sus **4 valores**:

1. **Individuos e interacciones** sobre procesos y herramientas.
2. **Software funcionando** sobre documentación extensiva.
3. **Colaboración con el cliente** sobre negociación contractual.
4. **Responder al cambio** sobre seguir un plan rígido.

> Agile promueve equipos autoorganizados, planificación adaptativa, entregas tempranas y mejora continua.

## El problema: Agile sin Operaciones

Implementar Agile sin integrar Ops genera problemas clave:

- **Desfase de velocidades:** Dev trabaja en sprints rápidos, pero Ops sigue procesos lentos y burocráticos (abrir tickets para recursos).
- **Retrasos en despliegues:** el código está listo, pero la entrega se demora porque Ops tarda en aprovisionar infraestructura o desplegar.
- **Frustración y pérdida de productividad:** la espera afecta la moral y la eficiencia del equipo.
- **"IT de dos velocidades" y Shadow IT:** para evitar esperas, los devs usan recursos externos (nube pública) **sin pasar por IT**, lo que genera riesgos de seguridad y falta de control.

## DevOps como solución

- Integra Agile en operaciones, **elimina silos** y acelera la entrega mediante la colaboración Dev + Ops.
- Promueve una cultura de **responsabilidad compartida y transparencia** para responder mejor al negocio.

> [!tip] Conclusión
> Agile por sí solo no basta: hay que integrar Operaciones para lograr entrega continua. Ese es el objetivo de DevOps.

## Para repasar

- [ ] ¿Quién creó XP y en qué año?
- [ ] Enuncia los 4 valores del Manifiesto Agile.
- [ ] ¿Qué es el "Shadow IT" y por qué es un riesgo?
- [ ] ¿Qué brecha cierra DevOps que Agile dejó abierta?

## Enlaces relacionados

- [[Modelo WaterFall]] — el problema previo que Agile vino a resolver.
- [[Caracteristicas Escenciales para DEVOPS]] — los tres pilares de la agilidad en DevOps.
- [[QA y DevOps]] — cómo encaja la calidad en este modelo.
