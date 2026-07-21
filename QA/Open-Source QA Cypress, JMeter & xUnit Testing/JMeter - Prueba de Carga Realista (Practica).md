---
tags: [devops, testing, performance-testing, jmeter, carga, practica]
alias: [Prueba de Carga Realista JMeter, Simulación de Usuarios Concurrentes]
creado: 2026-07-02
---

# JMeter — Prueba de Carga Realista (Práctica: múltiples endpoints)

> [!abstract] Resumen rápido
> Continuación práctica de [[Apache JMeter]]: se construye una prueba de carga más **realista**, simulando **10 usuarios concurrentes** que navegan por **varios endpoints** de un sitio (no solo una URL), con **pausas humanas** entre peticiones mediante un timer, y analizando la tasa de éxito/error por endpoint.

---

## 1. Configuración del Thread Group para esta prueba

| Parámetro | Valor usado | Resultado |
|---|---|---|
| Number of Threads (users) | 10 | 10 usuarios virtuales concurrentes |
| Loop Count | 3 | cada usuario repite el flujo 3 veces |
| Ramp-up period | 5 segundos | los 10 usuarios inician distribuidos en 5 s (~2 usuarios/segundo) |
| **Total de solicitudes por sampler** | **10 × 3 = 30** | cada HTTP Request configurado recibe 30 llamadas en total |

> [!example] Cálculo del total de requests
> Si el plan tiene **3 samplers HTTP** (por ejemplo `/`, `/contacts.php`, `/my_message.php`), el total real de solicitudes en toda la prueba es:
> `10 usuarios × 3 repeticiones × 3 endpoints = 90 solicitudes`.

### ¿Qué es exactamente un Thread Group?
Es el componente que define **cuántos usuarios virtuales** ("threads") ejecutan el plan de prueba, **cuántas veces** lo repiten, y **en qué intervalo de tiempo** arrancan. Es el punto donde se traduce "quiero simular X personas usando mi app" en una configuración concreta que JMeter puede ejecutar.

### Impacto del Ramp-up Period
- **Ramp-up corto** (ej. 1-2 segundos para 10 usuarios) → simula un **pico repentino** de tráfico (más parecido a un *spike test*), generando carga concentrada en poco tiempo.
- **Ramp-up más largo** (ej. 30-60 segundos) → simula una **llegada gradual** de usuarios, más parecida al tráfico orgánico real de una aplicación en producción.
- Un ramp-up demasiado corto respecto al número de usuarios puede generar **falsos cuellos de botella**: el sistema podría fallar no por falta de capacidad real, sino porque todos los usuarios llegaron literalmente al mismo milisegundo, algo poco realista fuera de eventos tipo "flash sale".

> [!tip] Regla práctica
> Un buen punto de partida es que el ramp-up (en segundos) sea aproximadamente igual o mayor al número de usuarios, para que cada usuario tenga al menos ~1 segundo de diferencia respecto al anterior al iniciar.

---

## 2. Endpoints: probar rutas distintas, no solo una URL

Un **endpoint** es una ruta específica de la aplicación a la que el usuario puede acceder (ej. `/`, `/contacts.php`, `/my_message.php`). Probar solo la home page no representa el comportamiento real de un usuario, que navega por **varias secciones**.

### Cómo se configuran múltiples HTTP Samplers
1. Se crea el primer **HTTP Request** apuntando al servidor base y a la ruta `/`.
2. Se **duplica** ese sampler (clic derecho → *Duplicate*) y se cambia solo el campo **Path** al siguiente endpoint (`/contacts.php`).
3. Se repite para cada ruta que se quiera simular en el recorrido del usuario.
4. Todos los samplers dentro del mismo Thread Group se ejecutan **en orden secuencial** dentro de cada iteración/loop, simulando la navegación de un usuario por el sitio.

> [!note] HTTP Request Defaults
> Para no repetir el dominio/servidor en cada sampler, conviene usar el elemento de configuración **HTTP Request Defaults**: se define ahí el servidor una sola vez, y cada sampler solo especifica su `Path` particular.

Ejemplo de recorrido típico simulado:

```
Usuario virtual:
  1. GET /                  → página principal
  2. GET /contacts.php      → formulario de contacto
  3. GET /my_message.php    → sección de mensajes
```

---

## 3. Simulando comportamiento humano: el Timer

Sin pausas, JMeter dispara las peticiones tan rápido como la red y el servidor lo permitan — algo que **ningún humano hace realmente** al navegar. Para corregirlo se añade un **Constant Timer** de, por ejemplo, **1000 ms (1 segundo)** entre cada sampler.

- Esto simula el tiempo que un usuario real tarda en leer la página, pensar y hacer clic en el siguiente enlace.
- Sin timer, la prueba mide más bien la **capacidad máxima teórica** del servidor (stress test), no el comportamiento bajo uso normal (load test).

### Variantes de timers más realistas
| Timer | Comportamiento |
|---|---|
| **Constant Timer** | Pausa fija (ej. siempre 1 s) — simple pero poco natural |
| **Uniform Random Timer** | Pausa aleatoria dentro de un rango — más variabilidad |
| **Gaussian Random Timer** | Pausa aleatoria con distribución normal — el patrón más parecido a comportamiento humano real |

---

## 4. Análisis de resultados por endpoint

Al ejecutar la prueba con listeners como **Summary Report** o **Aggregate Report**, JMeter desglosa las métricas **por cada sampler/endpoint por separado**, lo que permite comparar:

| Métrica | Qué indica |
|---|---|
| **# Samples** | Cuántas veces se ejecutó ese endpoint (debería ser 30 en el ejemplo de 10 usuarios × 3 loops) |
| **Average / Min / Max** | Tiempos de respuesta — permite ver si un endpoint específico es más lento que otros |
| **Error %** | Porcentaje de fallos — útil para detectar endpoints problemáticos bajo carga |
| **Throughput** | Peticiones por segundo procesadas para ese endpoint |

> [!important] Comparar entre endpoints, no solo mirar el total
> Si `/my_message.php` tiene un tiempo de respuesta mucho mayor que `/` y `/contacts.php`, eso apunta a un problema específico en esa ruta (ej. una consulta a base de datos lenta), algo que no se detectaría si solo se probara la página principal.

---

## 5. Probar rutas rotas: manejo de errores del servidor

Añadir intencionalmente un sampler apuntando a una **ruta inexistente** (ej. `/no-existe.php`) permite verificar:

- Que el servidor devuelva el **código de estado correcto** (ej. `404 Not Found`) en vez de un error genérico o un `500`.
- Que la aplicación **maneje el error de forma controlada** (página de error personalizada) y no exponga información sensible (stack traces, rutas internas del servidor).
- Cómo se comporta el sistema cuando, bajo carga real, algunos requests fallan legítimamente (enlaces rotos, recursos movidos, etc.) — es decir, si el manejo de errores sigue siendo estable incluso cuando el servidor está bajo estrés.

Esto convierte la prueba de rendimiento también en una verificación básica de **resiliencia** y manejo de errores, no solo de velocidad.

---

## 6. Buenas prácticas reforzadas en esta práctica

- Usar **HTTP Request Defaults** para no repetir el servidor en cada sampler.
- Nombrar claramente cada sampler (ej. "Home Page", "Formulario de Contacto") para que los reportes sean legibles.
- Incluir siempre al menos un **timer** cuando se busca simular carga realista (load test), y omitirlo deliberadamente solo si se busca un stress test puro.
- Revisar métricas **por endpoint**, no solo el resumen agregado de toda la prueba.
- Incluir deliberadamente algún endpoint que falle, para validar el manejo de errores del sistema bajo prueba.

---

## 7. Preguntas para repasar (auto-evaluación)

- [ ] ¿Cómo se calcula el número total de solicitudes dado un número de usuarios, loops y endpoints?
- [ ] ¿Qué diferencia hay entre un ramp-up corto y uno largo, en términos de qué tipo de prueba estás simulando?
- [ ] ¿Para qué sirve HTTP Request Defaults al trabajar con múltiples samplers?
- [ ] ¿Por qué un Constant Timer hace la prueba más realista?
- [ ] ¿Qué se puede aprender al incluir un endpoint roto (404) en la prueba de carga?

---

## 8. Recursos recomendados para profundizar

- 🌐 [Documentación oficial — Thread Group](https://jmeter.apache.org/usermanual/component_reference.html#Thread_Group)
- 🌐 [Documentación oficial — Timers](https://jmeter.apache.org/usermanual/component_reference.html#timers)
- 🌐 Sitios públicos diseñados para practicar pruebas de carga, como *blazedemo.com* o *demoblaze.com* (verificar siempre que el sitio permita explícitamente pruebas de carga antes de usarlo).
- 🌐 [JMeter Best Practices (oficial)](https://jmeter.apache.org/usermanual/best-practices.html)

---

## 9. Notas relacionadas
- [[Apache JMeter]]
- [[CI-CD Pipeline]]
- [[Microservicios Nativos en la Nube]]
- [[TDD - Test-Driven Development]]
- [[BDD - Behavior-Driven Development]]

---
#devops #testing #jmeter #performance-testing #carga #practica
