---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 2 - Estrategias de Testing Agile
tema: Fundamentos de la automatización de pruebas
fecha: 2026-06-22
fuente: https://www.coursera.org/learn/qa-process-optimization-agile-automated-testing/lecture/NCxKu/foundations-of-test-automation
tags: [qa, automatizacion, piramide-pruebas, unit-test, e2e, integracion]
---

# Fundamentos de la automatización de pruebas

> [!info] Idea central
> Existen varios tipos de pruebas automatizadas. La **pirámide de pruebas** indica cómo **distribuir el esfuerzo**: muchas pruebas baratas en la base, pocas y costosas en la cima.

## Tipos de pruebas automatizadas

- **Pruebas unitarias:** verifican piezas pequeñas de código (funciones o métodos) **de forma aislada**.
- **Pruebas de API e integración:** validan la comunicación y la correcta interacción entre componentes o sistemas vía interfaces de programación.
- **Pruebas end-to-end (E2E):** simulan interacciones de usuario para validar **procesos de negocio completos** y comprobar que todo funciona junto.
- **Pruebas visuales:** comparan **capturas de pantalla** para detectar cambios inesperados en la UI; funcionan como pruebas rápidas de humo.

## La pirámide de pruebas

```
            ▲  más costosas / lentas / pocas
           /E2E\        ← procesos de negocio críticos
          /------\
         /Integr. \     ← interacciones críticas entre componentes
        /----------\
       /  Unitarias  \  ← rápidas, baratas, cubren la mayor parte del código
      ────────────────  más baratas / rápidas / muchas
```

| Nivel | Coste | Velocidad | Cobertura |
|:--|:--|:--|:--|
| Unitarias (base) | Bajo | Rápidas | Gran parte del código |
| Integración (medio) | Medio | Media | Interacciones críticas |
| E2E (cima) | Alto | Lentas | Procesos de negocio críticos |

## Balance y aplicación práctica

- **No automatizar todo con E2E:** son caras de crear y mantener.
- La combinación adecuada según la pirámide ayuda a **mantener la calidad** y a detectar errores en distintos niveles.

> [!warning] Antipatrón
> Invertir la pirámide (muchos E2E, pocas unitarias) produce suites lentas, frágiles y caras de mantener.

## Para repasar

- [ ] ¿Qué prueba aísla una única función o método?
- [ ] ¿Por qué las E2E van en la cima de la pirámide?
- [ ] ¿Qué problema causa "invertir" la pirámide de pruebas?

## Enlaces relacionados

- [[Agile Test Scenarios Management]] — cuándo conviene automatizar un caso.
- [[TDD AND BDD]] — escribir las pruebas antes que el código.
- [[Métricas y KPIs para QA Agile]] — cómo medir la cobertura resultante.
