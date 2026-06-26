---
curso: QA Process Optimization, Agile & Automated Testing
modulo: 2 - Estrategias de Testing Agile
tema: TDD y BDD
fecha: 2026-06-22
fuente: https://www.coursera.org/learn/qa-process-optimization-agile-automated-testing/lecture/UT2kl/tdd-bdd
tags: [qa, tdd, bdd, three-amigos, gherkin]
---

# TDD y BDD

> [!info] Idea central
> Alinearse **temprano** mediante pruebas inteligentes ahorra tiempo y reduce confusiones. **TDD** se centra en el código correcto; **BDD** extiende TDD hacia el **comportamiento** y la colaboración.

## Test-Driven Development (TDD)

Se escriben las **pruebas antes** del código funcional, siguiendo el ciclo **rojo-verde-refactor**:

```
🔴 ROJO      → escribe una prueba que falla
🟢 VERDE     → escribe el código mínimo para que pase
🔵 REFACTOR  → mejora el código sin romper la prueba
```

## Behavior-Driven Development (BDD)

- **Extiende TDD** enfocándose en el **comportamiento** de la aplicación.
- Fomenta la **colaboración** entre desarrolladores, testers y stakeholders.
- Usa escenarios legibles en **lenguaje natural** con el formato **dado-cuando-entonces** (*given-when-then*) para definir expectativas claras y aceptación.

> [!example] Escenario BDD (Gherkin)
> **Dado** que el usuario tiene saldo suficiente
> **Cuando** solicita un retiro válido
> **Entonces** el sistema entrega el dinero y descuenta el saldo

## Colaboración: los "Three Amigos"

- El modelo **Three Amigos** reúne a **negocio, desarrollo y testing** para definir requisitos y criterios de aceptación **antes** de empezar a codificar.
- Asegura que todos entiendan y acuerden **cómo se probará y validará** la funcionalidad → mejor calidad y predictibilidad.

## TDD vs BDD

| | TDD | BDD |
|:--|:--|:--|
| **Enfoque** | Código correcto | Comportamiento esperado |
| **Lenguaje** | Técnico (código) | Natural (*given-when-then*) |
| **Público** | Desarrolladores | Negocio + Dev + Testing |

## Para repasar

- [ ] Describe el ciclo rojo-verde-refactor.
- [ ] ¿Qué añade BDD respecto a TDD?
- [ ] ¿Quiénes son los "Three Amigos" y cuándo se reúnen?

## Enlaces relacionados

- [[Criteria and Definition of Done]] — los criterios de aceptación que BDD formaliza.
- [[Foundations of test Automation]] — TDD alimenta la base de la pirámide (unitarias).
- [[Cómo medir la calidad pragmáticamente]] — propone BDD para medir calidad técnica.
