<div align="center">
<img src="./assets/header_esp.png" alt="GitHub Copilot - Programa de Adopción" width="100%" />

# 🤖 Workshop 2 — GitHub Copilot CLI: Agentes, Git, MCP y Extensibilidad

**Hands-on de issue → fix → test → PR, GitHub MCP, AGENTS.md y Agent Skills**

**⏱️ Duración total: 90 minutos**

</div>

---

Este workshop concentra el contenido práctico de los módulos M2 y M3 en **seis laboratorios de 15 minutos**. El participante trabaja con el agente como ejecutor de tareas reales: resolver issues, investigar bugs, generar tests, operar GitHub desde lenguaje natural, definir instrucciones persistentes y construir una pequeña aplicación guiada por una skill de brainstorming.

> [!TIP]
> El workshop asume que GitHub Copilot CLI ya está instalado, autenticado y ejecutándose dentro del repositorio de práctica. Los prerrequisitos no consumen los 90 minutos del laboratorio.

---

## 📋 Tabla de Contenidos

1. [🎯 Objetivos de aprendizaje](#-objetivos-de-aprendizaje)
2. [⏱️ Duración estimada](#️-duración-estimada)
3. [📚 Requisitos previos](#-requisitos-previos)
4. [🛠️ LAB 2A. Fix + PR completo desde el CLI](#️-lab-2a-fix--pr-completo-desde-el-cli)
5. [🕵️ LAB 2B. Bug Hunter](#️-lab-2b-bug-hunter)
6. [🧪 LAB 2C. Tests automáticos con el agente](#-lab-2c-tests-automáticos-con-el-agente)
7. [🔌 LAB 3A. GitHub MCP en lenguaje natural](#-lab-3a-github-mcp-en-lenguaje-natural)
8. [📜 LAB 3B. AGENTS.md y reglas persistentes](#-lab-3b-agentsmd-y-reglas-persistentes)
9. [💡 LAB 3C. Brainstorming y scaffolding de una app](#-lab-3c-brainstorming-y-scaffolding-de-una-app)
10. [✅ Checklist de finalización](#-checklist-de-finalización)
11. [🧭 Reflexiones finales](#-reflexiones-finales)

---

## 🎯 Objetivos de aprendizaje

Al finalizar este taller serás capaz de:

- ✅ Resolver un issue con Copilot CLI y completar el flujo **branch → cambio → commit → push → PR**.
- ✅ Utilizar el agente para investigar un bug a partir del último commit.
- ✅ Aplicar un flujo **test rojo → fix → suite verde**.
- ✅ Controlar herramientas del agente mediante `--allow-tool` y `--deny-tool`.
- ✅ Operar issues y GitHub Actions desde el CLI utilizando las capacidades nativas de GitHub MCP.
- ✅ Crear un `AGENTS.md` con convenciones de commits, estilo de código y restricciones críticas.
- ✅ Validar que las instrucciones persistentes afectan el comportamiento del agente.
- ✅ Utilizar una Agent Skill de brainstorming para pasar de una idea a spec, plan y scaffolding.

---

## ⏱️ Duración estimada

| Laboratorio | Tiempo |
| --- | ---: |
| 🛠️ LAB 2A — Fix + PR | 15 min |
| 🕵️ LAB 2B — Bug Hunter | 15 min |
| 🧪 LAB 2C — Tests automáticos | 15 min |
| 🔌 LAB 3A — GitHub MCP | 15 min |
| 📜 LAB 3B — AGENTS.md | 15 min |
| 💡 LAB 3C — Brainstorming | 15 min |
| **Total** | **90 min** |

> [!IMPORTANT]
> Para respetar los 90 minutos, cada bloque tiene timebox estricto. Si una operación remota (push, PR, GitHub Actions o agente cloud) demora más de lo previsto, continuá con el checkpoint local y retomá la validación remota al final.

---

## 📚 Requisitos previos

Antes de comenzar:

- GitHub Copilot CLI debe estar instalado y autenticado.
- El repositorio del workshop debe estar clonado localmente.
- Debés poder ejecutar `git pull`, crear branches y ejecutar los tests del proyecto.
- Para los pasos que crean issues o PRs necesitás permisos suficientes sobre el repositorio.
- El CLI debe ejecutarse dentro del directorio del repositorio.

> [!NOTE]
> La transcripción indica que algunos participantes pueden no tener permisos para completar el push/PR en un tenant corporativo. En ese caso, el flujo puede practicarse sobre una copia o repositorio personal autorizado por el instructor.

---

## 🛠️ LAB 2A. Fix + PR completo desde el CLI

**⏱️ 15 minutos**

**Objetivo:** delegar al agente un bug documentado en GitHub y completar un Pull Request sin salir de la terminal.

### 1. Abrir Copilot CLI

Desde el repositorio:

```bash
copilot
```

Trabajá en **Modo Normal** para poder revisar cada acción.

### 2. Consultar issues abiertos

Enviá:

```text
¿Qué issues abiertos tiene este repositorio?
```

### 3. Elegir un bug

Seleccioná uno de los bugs documentados en los issues.

El material utiliza como ejemplo un problema en `validateEmail` que no valida subdominios. Si ese issue está disponible, podés utilizar un prompt equivalente a:

```text
Hay un bug en validateEmail: no valida subdominios.
Corrígelo, crea la rama fix/validate-email y abre un PR.
```

### 4. Revisar cada acción

En Modo Normal, verificá que el agente proponga o ejecute con tu aprobación un flujo equivalente a:

```text
1. Inspeccionar el archivo afectado.
2. Modificar la implementación.
3. Crear una rama de fix.
4. Agregar los cambios a Git.
5. Crear un commit.
6. Hacer push de la rama.
7. Crear un Pull Request.
```

### 5. Validar el PR

Abrí GitHub.com y confirmá que el Pull Request fue creado correctamente.

### Checkpoint

- [ ] Issue identificado.
- [ ] Rama creada.
- [ ] Cambio revisado.
- [ ] Commit creado.
- [ ] PR creado o flujo preparado hasta el límite permitido por tu entorno.

> [!TIP]
> El objetivo no es aceptar todo automáticamente. Observá qué herramientas solicita utilizar el agente y qué comando Git propone en cada etapa.

---

## 🕵️ LAB 2B. Bug Hunter

**⏱️ 15 minutos**

**Objetivo:** investigar un cambio reciente, probar el bug antes de corregirlo y cerrar el ciclo con tests.

### 1. Traer el último cambio

```bash
git pull
```

### 2. Pedir análisis del último commit

```text
Analiza el último commit. ¿Qué cambió y hay algún problema?
```

Leé el diagnóstico. **No apruebes cambios todavía.**

### 3. Probar primero el bug

```text
Escribe un test que falle si el bug existe. Ejecútalo.
```

### Resultado esperado

Debés observar un test **en rojo** que reproduzca el problema.

> [!IMPORTANT]
> No continúes con el fix hasta tener evidencia de que el test realmente falla por el bug identificado.

### 4. Corregir y ejecutar la suite

```text
Corrígelo. Corre el suite completo, sin regresiones.
```

### 5. Crear el PR

```text
Abre un PR con el fix describiendo el bug encontrado.
```

### Checkpoint

- [ ] El agente explicó el último commit.
- [ ] El bug fue reproducido mediante un test fallido.
- [ ] El fix hizo pasar el test.
- [ ] La suite completa fue ejecutada.
- [ ] El PR documenta el problema encontrado.

---

## 🧪 LAB 2C. Tests automáticos con el agente

**⏱️ 15 minutos**

**Objetivo:** comparar el flujo interactivo tradicional con una sesión en la que se pre-aprueba `shell` pero se bloquea una operación riesgosa.

### 1. Lanzar Copilot con control de tools

Salí de la sesión actual si fuese necesario y ejecutá:

```bash
copilot --allow-tool='shell' --deny-tool='shell(rm)'
```

### 2. Identificar funciones sin tests

```text
Identifica funciones en src/ que no tengan cobertura de tests.
```

### 3. Generar los tests faltantes

```text
Escribe los tests faltantes utilizando el framework de testing que ya usa este proyecto.
```

### 4. Ejecutar y validar

```text
Ejecuta los tests y verifica que todos pasen.
```

Si existe un fallo:

```text
Diagnostica por qué falla el test y corrígelo sin eliminar la cobertura que acabas de agregar.
```

### 5. Comparar fluidez

Compará esta experiencia con una sesión sin `--allow-tool='shell'`.

### Resultado esperado

El agente puede ejecutar comandos shell autorizados con menos interrupciones, mientras que `shell(rm)` permanece explícitamente denegado.

### Checkpoint

- [ ] Se identificaron funciones sin tests.
- [ ] Se agregaron tests utilizando el framework del proyecto.
- [ ] La suite fue ejecutada.
- [ ] Entendiste la diferencia entre permitir una tool y bloquear una sub-operación.

---

## 🔌 LAB 3A. GitHub MCP en lenguaje natural

**⏱️ 15 minutos**

**Objetivo:** gestionar recursos GitHub desde el CLI mediante lenguaje natural.

### 1. Habilitar los toolsets disponibles de GitHub MCP

```bash
copilot --enable-all-github-mcp-tools
```

### 2. Listar issues

Dentro de Copilot:

```text
Lista todos los issues abiertos de este repositorio.
```

También podés probar:

```text
¿Qué issues abiertos están asignados a mí?
```

### 3. Crear un issue desde la terminal

Usá una descripción clara. El material muestra como ejemplo:

```text
Crea un issue: "Rate limiting en /login" con label "security".
```

### 4. Revisar GitHub Actions

Ejecutá:

```text
/view actions
```

### 5. Asignar un issue

Por ejemplo:

```text
Asigna el issue #12 a mi usuario.
```

Reemplazá `#12` por un issue válido del repositorio.

### 6. Observar delegación con `&`

Si tu plan y las políticas del entorno lo permiten, probá:

```text
& Implementa el rate limiting del issue #12
```

### Resultado esperado

Debés comprobar que el agente puede consultar y operar recursos de GitHub utilizando herramientas nativas, sin necesidad de navegar manualmente por la UI para cada operación.

> [!NOTE]
> La delegación con `&` puede depender del plan y de las políticas habilitadas para la organización. Si no está disponible, registrá la respuesta del CLI y continuá con el siguiente laboratorio.

---

## 📜 LAB 3B. AGENTS.md y reglas persistentes

**⏱️ 15 minutos**

**Objetivo:** crear instrucciones de repositorio que definan cómo debe comportarse el agente al trabajar con el proyecto.

### 1. Pedir una propuesta basada en el repo

```text
Genera un AGENTS.md basado en las convenciones que observas en el código.
```

### 2. Revisar y ajustar

El archivo debe contener, como mínimo:

- Convención de commits.
- Convención de nombres de branches.
- Estilo de código.
- Reglas de testing.
- Al menos una restricción crítica.

El material usa como referencia:

```markdown
# AGENTS.md — Proyecto API

## Commits y branches
- Conventional Commits: feat:, fix:, chore:, docs:, test:
- Branch naming: feature/, fix/, chore/, docs/
- NUNCA push directo a main o develop

## Estilo de código
- TypeScript estricto, sin `any`
- Tests con Jest usando patrón describe/it
- Coverage mínimo 80%
- JSDoc obligatorio en funciones públicas

## Restricciones críticas
- NO modificar /migrations sin confirmación explícita del usuario
- NO ejecutar scripts que afecten la base de datos en producción
```

> [!NOTE]
> Conservá únicamente las reglas que tengan sentido para el repositorio real. El ejemplo es una plantilla de referencia, no una orden para inventar tecnologías o convenciones que el proyecto no utiliza.

### 3. Reiniciar el agente

Guardá el archivo y reiniciá la sesión según lo indicado por el material:

```text
/restart
```

### 4. Probar la regla de commits

Pedí al agente crear un commit de un cambio controlado y verificá que siga **Conventional Commits**.

### 5. Bonus: crear un Skill básico

La ubicación por repositorio mostrada en el material es:

```text
.github/skills/MI-SKILL/SKILL.md
```

Un frontmatter mínimo puede contener los campos que el material describe:

```yaml
---
name: mi-skill
description: Describe cuándo y para qué debe utilizarse esta skill
allowed-tools: [shell]
user-invocable: true
---
```

Luego agregá instrucciones Markdown debajo del frontmatter e intentá invocarla con el slash command correspondiente.

### Checkpoint

- [ ] `AGENTS.md` creado y revisado.
- [ ] Convenciones reales del repo documentadas.
- [ ] Restricción crítica incluida.
- [ ] Sesión reiniciada.
- [ ] Comportamiento del agente validado con al menos una regla.

---

## 💡 LAB 3C. Brainstorming y scaffolding de una app

**⏱️ 15 minutos**

**Objetivo:** pasar rápidamente de una idea a una especificación, un plan y un scaffolding utilizando una skill de brainstorming.

### 1. Elegir una idea

El material propone tres ejemplos:

- `prompt vault`
- `dev log diario`
- `tech debt board`

También podés elegir otra idea simple aprobada por el instructor.

### 2. Mantener las restricciones técnicas del laboratorio

La aplicación debe utilizar:

```text
Next.js 15
Server Functions
Base de datos local
```

### 3. Pedir scaffolding

En Copilot, pedí ayuda para crear la estructura inicial de la aplicación respetando esas restricciones.

Ejemplo de prompt derivado del laboratorio:

```text
Quiero crear una aplicación <IDEA>.
Debe estar desarrollada en Next.js 15, usar Server Functions y una base de datos local.
Primero proponé el scaffolding del proyecto. No agregues tecnologías que no sean necesarias para estos requisitos.
```

### 4. Crear spec mediante brainstorming

Invocá la skill `brainstorming` instalada para el workshop y utilizala para convertir la idea en una especificación suficientemente clara.

La transcripción destaca que el flujo puede hacer preguntas y proponer distintas direcciones antes de cerrar la especificación.

### 5. Generar un plan

Una vez aceptada la spec, pedí que el agente produzca el plan de implementación antes de construir.

### 6. Implementar y preparar PR

Dejá que el agente complete el scaffolding dentro del timebox y pedí finalmente que prepare un PR hacia `main`, sin hacer push directo a `main`.

### Resultado esperado

Al final de los 15 minutos deberías contar al menos con:

- Una idea elegida.
- Una spec generada mediante brainstorming.
- Un plan de implementación.
- Un scaffolding inicial funcional o en progreso.
- Un flujo de PR preparado o completado según permisos y tiempo.

> [!TIP]
> El objetivo de este laboratorio no es terminar un producto completo. Es practicar el ciclo **idea → preguntas → spec → plan → ejecución** dentro de una sesión agéntica.

---

## ✅ Checklist de finalización

- [ ] Un issue fue utilizado como entrada para un fix.
- [ ] Se practicó el ciclo test rojo → fix → suite verde.
- [ ] Se probaron `--allow-tool` y `--deny-tool`.
- [ ] Se operaron issues o Actions mediante GitHub MCP.
- [ ] Se creó y validó un `AGENTS.md`.
- [ ] Se comprendió la diferencia entre `AGENTS.md` y un Skill reutilizable.
- [ ] Se creó una spec y un plan desde una idea usando brainstorming.
- [ ] Se preparó al menos un flujo de Pull Request.

---

## 🧭 Reflexiones finales

- El agente puede encargarse de un flujo Git completo, pero el desarrollador sigue siendo responsable de revisar los cambios y permisos utilizados.
- El patrón **test primero, fix después** permite verificar que el agente está corrigiendo el problema correcto.
- `--allow-tool` mejora fluidez; `--deny-tool` permite mantener límites explícitos.
- GitHub MCP acerca issues, PRs y Actions al mismo flujo de terminal.
- `AGENTS.md` contiene reglas persistentes del repositorio; los Skills encapsulan procedimientos reutilizables que se cargan cuando son relevantes.
- Un buen flujo agéntico empieza con una especificación clara y un plan revisable antes de delegar implementación.

---