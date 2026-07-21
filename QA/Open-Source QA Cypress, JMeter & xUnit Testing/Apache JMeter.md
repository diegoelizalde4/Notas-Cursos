---
tags: [devops, testing, performance-testing, jmeter, carga]
alias: [JMeter, Apache JMeter, Pruebas de Rendimiento]
creado: 2026-07-02
---

# Apache JMeter — Pruebas de Rendimiento

> [!abstract] Resumen rápido
> **Apache JMeter** es una herramienta open-source escrita en Java para realizar **pruebas de rendimiento (performance testing)**, simulando múltiples usuarios virtuales que ejecutan peticiones (HTTP, entre otras) contra un sistema, con el fin de medir tiempos de respuesta, throughput y detectar fallos bajo carga.

---

## 1. Instalación y configuración

- **Requisito**: Java 8 o superior (JMeter corre sobre la JVM).
- Se descarga desde el sitio oficial: [jmeter.apache.org](https://jmeter.apache.org/download_jmeter.cgi).
- Se descomprime el `.zip`/`.tgz` y se ejecuta:
  - **Windows**: `bin/jmeter.bat`
  - **Linux/macOS**: `bin/jmeter.sh` (o `./jmeter` desde terminal)
- Se abre la **GUI** de JMeter para construir el plan de prueba. En entornos de CI/CD normalmente se ejecuta en **modo no-GUI** (ver sección 6).

> [!warning] La GUI no es para ejecutar pruebas reales
> La interfaz gráfica sirve para **diseñar y depurar** el plan de prueba. Para pruebas de carga reales (muchos usuarios), JMeter recomienda ejecutar en **modo consola/no-GUI**, ya que la GUI consume recursos que distorsionan los resultados.

---

## 2. Estructura de un plan de prueba (Test Plan)

El **Test Plan** es el contenedor raíz donde se organiza toda la prueba. Su jerarquía típica:

```
Test Plan
└── Thread Group (Grupo de hilos)
    ├── HTTP Request Defaults (opcional)
    ├── HTTP Request (Sampler)
    ├── Timers (opcional)
    ├── Assertions (opcional)
    └── Listeners (View Results Tree, Summary Report, etc.)
```

### Thread Group (Grupo de hilos)
Simula a los **usuarios virtuales**. Cada "hilo" (thread) representa un usuario concurrente ejecutando el flujo de prueba. Parámetros principales:

| Parámetro | Qué controla |
|---|---|
| **Number of Threads (users)** | Cuántos usuarios virtuales simultáneos |
| **Ramp-up period** | Tiempo (segundos) en que JMeter va "arrancando" a todos los usuarios, de forma gradual |
| **Loop Count** | Cuántas veces cada usuario repite el flujo completo |

> [!example] Ejemplo: 20 usuarios, 3 repeticiones
> - Number of Threads: `20`
> - Loop Count: `3`
> - Ramp-up period: por ejemplo `10` segundos → JMeter añadirá ~2 usuarios nuevos cada segundo hasta llegar a 20, evitando que todos arranquen exactamente al mismo instante (lo cual generaría un pico artificial no realista).
> - Total de peticiones = 20 usuarios × 3 repeticiones × (peticiones por flujo).

### Sampler — HTTP Request
Define la **acción concreta** que ejecuta cada usuario virtual: a qué URL/endpoint hace la petición, con qué método (GET, POST, etc.), parámetros, headers, body, etc. Un Thread Group puede contener varios samplers para simular un flujo completo (ej: login → navegar catálogo → agregar al carrito → checkout).

### Listeners
Componentes que **visualizan y almacenan los resultados** de la ejecución:

| Listener | Uso típico |
|---|---|
| **View Results Tree** | Detalle petición por petición (request/response), útil para depurar. **No usar en pruebas de carga reales** (consume mucha memoria). |
| **Summary Report** | Resumen agregado: promedio, mínimo, máximo, throughput, % error por sampler. |
| **Aggregate Report** | Similar al Summary, con percentiles (útil para SLAs, ej. p90, p95, p99). |
| **Response Time Graph** | Gráfico de tiempos de respuesta a lo largo de la prueba. |

---

## 3. Ejecución y análisis de resultados

Al correr la prueba, JMeter reporta por cada request:

- **Código de estado HTTP** (200, 404, 500, etc.) → detecta errores funcionales bajo carga.
- **Response time (tiempo de respuesta)**: cuánto tarda el servidor en responder.
- **Throughput**: peticiones procesadas por unidad de tiempo (ej. requests/segundo).
- **% Error**: porcentaje de peticiones fallidas.
- **Latency vs Connect Time**: latencia de red vs tiempo de establecer la conexión.

> [!tip] Qué buscar
> Un aumento de usuarios virtuales que hace crecer el tiempo de respuesta de forma lineal es esperable; un crecimiento **exponencial** o un aumento repentino en la tasa de error suele indicar que se alcanzó el **punto de saturación** del sistema (cuello de botella en CPU, memoria, conexiones a BD, etc.).

---

## 4. Conceptos complementarios (no cubiertos en el resumen original)

### 4.1 Tipos de pruebas de rendimiento
JMeter permite ejecutar distintos tipos de prueba según cómo se configure el Thread Group:

| Tipo de prueba | Objetivo | Cómo se configura en JMeter |
|---|---|---|
| **Load Testing** | Verificar comportamiento bajo carga esperada normal | Usuarios = carga típica de producción |
| **Stress Testing** | Encontrar el punto de quiebre del sistema | Aumentar usuarios progresivamente hasta que falle |
| **Spike Testing** | Ver cómo reacciona el sistema a picos súbitos de tráfico | Ramp-up muy corto (usuarios entran casi de golpe) |
| **Soak / Endurance Testing** | Detectar degradación en el tiempo (memory leaks, etc.) | Carga moderada sostenida por horas |

### 4.2 Timers
Los **Timers** introducen pausas entre peticiones para simular el comportamiento humano real (nadie hace clics instantáneos sin pensar). El más común es **Constant Timer** o **Gaussian Random Timer**, evitando que la prueba genere una carga artificialmente agresiva.

### 4.3 Assertions
Permiten validar que la respuesta sea **correcta**, no solo que responda con código 200. Ejemplos:
- **Response Assertion**: verifica que el body contenga cierto texto.
- **Duration Assertion**: falla si la respuesta tarda más de X ms.

Esto conecta el performance testing con la validación funcional bajo carga.

### 4.4 Correlación y manejo de variables dinámicas
En flujos reales (login con token de sesión, CSRF tokens, IDs generados dinámicamente), es necesario **extraer valores de una respuesta y reutilizarlos** en la siguiente petición. Se logra con:
- **Regular Expression Extractor**
- **JSON Extractor** (para APIs REST que responden JSON)
- Variables JMeter (`${nombreVariable}`)

### 4.5 CSV Data Set Config
Permite alimentar el test con datos externos (ej. lista de usuarios/contraseñas desde un `.csv`), para que cada hilo use datos distintos en vez de repetir siempre el mismo usuario — más realista.

### 4.6 Modo No-GUI (para CI/CD)
Para integrarlo en un pipeline de DevOps (CI/CD), JMeter se ejecuta por línea de comandos:

```bash
jmeter -n -t plan_de_prueba.jmx -l resultados.jtl -e -o reporte_html/
```

- `-n`: modo no-GUI
- `-t`: archivo del plan de prueba (`.jmx`)
- `-l`: archivo de resultados
- `-e -o`: genera automáticamente un **reporte HTML** con dashboards

Esto permite ejecutar pruebas de rendimiento automáticamente en cada release, como parte de un pipeline de **Continuous Testing**, y fallar el build si se superan ciertos umbrales de tiempo de respuesta o tasa de error.

### 4.7 Distributed Testing (pruebas distribuidas)
Cuando se necesita simular una cantidad de usuarios muy alta (miles), una sola máquina puede no dar abasto (ni ser representativa de tráfico real distribuido). JMeter soporta **modo maestro-esclavo (master-slave)**: varias máquinas ("slaves") generan carga coordinadas por un nodo maestro que consolida los resultados.

### 4.8 Alternativas a JMeter
| Herramienta | Características |
|---|---|
| **Gatling** | Basado en Scala, scripts como código, buen rendimiento con menos recursos |
| **k6** | Moderno, scripts en JavaScript, muy usado en pipelines CI/CD cloud-native |
| **Locust** | Basado en Python, define usuarios como código |
| **Apache Bench (ab)** | Muy simple, solo para pruebas HTTP básicas |

---

## 5. Buenas prácticas

- Ejecutar las pruebas de carga reales en **modo no-GUI**, no desde la interfaz.
- Definir un **ramp-up realista** en vez de lanzar todos los usuarios de golpe (salvo que se busque explícitamente un *spike test*).
- Monitorear también el **servidor bajo prueba** (CPU, memoria, conexiones a BD) durante la ejecución, no solo los resultados desde JMeter.
- Parametrizar datos con **CSV Data Set Config** para evitar que todos los usuarios virtuales sean idénticos.
- Integrar JMeter al pipeline de CI/CD para detectar regresiones de rendimiento automáticamente en cada despliegue.

---

## 6. Preguntas para repasar (auto-evaluación)

- [ ] ¿Qué es un Thread Group y qué tres parámetros principales lo configuran?
- [ ] ¿Cómo configuraría un test plan para simular 20 usuarios con 3 repeticiones?
- [ ] ¿Por qué no se recomienda usar la GUI de JMeter para correr pruebas de carga reales?
- [ ] ¿Qué diferencia hay entre un Load Test y un Stress Test?
- [ ] ¿Para qué sirve un Regular Expression Extractor?

---

## 7. Recursos recomendados para profundizar

- 🌐 [Documentación oficial de Apache JMeter](https://jmeter.apache.org/usermanual/index.html)
- 🌐 [JMeter Best Practices](https://jmeter.apache.org/usermanual/best-practices.html) (guía oficial)
- 📘 *Apache JMeter: A practical beginner's guide* — varios autores en editoriales de testing técnico
- 🌐 Comparativa [k6 vs JMeter vs Gatling](https://k6.io/blog/comparing-best-open-source-load-testing-tools) — útil para elegir herramienta según contexto cloud-native

---

## 8. Notas relacionadas
- [[TDD - Test-Driven Development]]
- [[BDD - Behavior-Driven Development]]
- [[CI-CD Pipeline]]
- [[Microservicios Nativos en la Nube]]
- [[Pirámide de Testing]]

---
#devops #testing #jmeter #performance-testing #carga
