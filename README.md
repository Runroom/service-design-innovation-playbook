# AI Innovation Playbook — Skills para diseño de servicio con IA

Conjunto de **18 Agent Skills** que operacionalizan un playbook completo de innovación en servicios con IA: descubrir, definir, idear y validar. Cada skill cubre una habilidad concreta del proceso de service design, con su entrada mínima, mentalidad activa, guardarraíles y entregable esperado.

Está pensado para equipos de diseño, producto e innovación que trabajan con Claude (Claude Code, Claude Desktop, claude.ai) y quieren incorporar prácticas rigurosas de **service design** y **design thinking aplicado a IA** dentro de su flujo de trabajo.

[![skills.sh](https://skills.sh/b/jose-saura/ai-innovation-playbook-skills)](https://skills.sh/jose-saura/ai-innovation-playbook-skills)

## Instalación

Las skills siguen el estándar abierto [Agent Skills](https://agentskills.io), por lo que funcionan en cualquier harness compatible. Para los harness que no lo soporten nativamente, hay instrucciones de adaptación más abajo.

### Vía skills.sh (recomendado, multi-harness)

```bash
npx skills add <owner>/<repo>
```

> Sustituye `<owner>/<repo>` por el slug real de GitHub cuando publiques el repositorio.

`skills.sh` instala las skills en `~/.claude/skills/` o `~/.agents/skills/` según el harness detectado.

---

### Claude Code · Claude Desktop · claude.ai

**Claude Code (CLI):**

```bash
git clone https://github.com/<owner>/<repo>.git
cp -r <repo>/skills/* ~/.claude/skills/        # usuario (todos los proyectos)
# o, dentro de un proyecto concreto:
cp -r <repo>/skills/* .claude/skills/
```

**Claude Desktop / claude.ai:**

Pega el contenido del `SKILL.md` que necesites en el campo de instrucciones del proyecto o en la conversación. Para la guía orquestadora, pega [`skills/playbook-guia/SKILL.md`](skills/playbook-guia/SKILL.md).

---

### OpenAI Codex CLI

Codex soporta Agent Skills nativamente desde su lanzamiento más reciente. Detecta skills en `.agents/skills/` (workspace) y `~/.agents/skills/` (usuario), exactamente la misma ruta que Gemini CLI.

**Usuario (disponibles en todos los proyectos):**

```bash
git clone https://github.com/<owner>/<repo>.git
mkdir -p ~/.agents/skills
cp -r <repo>/skills/* ~/.agents/skills/
```

**Workspace (compartido vía git con tu equipo):**

```bash
mkdir -p .agents/skills
cp -r <ruta-al-repo>/skills/* .agents/skills/
```

Codex también busca en `.agents/skills/` recorriendo el árbol desde el directorio actual hasta la raíz del repo, así que basta con tener la carpeta en cualquier punto del path.

---

### Google Gemini CLI

Gemini CLI soporta Agent Skills nativamente y acepta el mismo alias `.agents/skills/`.

**Usuario:**

```bash
git clone https://github.com/<owner>/<repo>.git
mkdir -p ~/.gemini/skills
cp -r <repo>/skills/* ~/.gemini/skills/
# o, alternativa cross-tool:
cp -r <repo>/skills/* ~/.agents/skills/
```

**Workspace:**

```bash
mkdir -p .gemini/skills
cp -r <ruta-al-repo>/skills/* .gemini/skills/
# o, alternativa cross-tool:
cp -r <ruta-al-repo>/skills/* .agents/skills/
```

Una vez copiadas, dentro de una sesión de Gemini CLI:

```text
/skills reload
/skills list
```

Para enlazar sin copiar:

```bash
gemini  # entra en sesión
> /skills link <ruta-al-repo>/skills --scope user
```

---

### Instalación interoperable (Codex + Gemini + cualquier harness que use el alias `.agents/`)

Si quieres que las skills funcionen en **todos los harness compatibles** desde una única ubicación:

```bash
mkdir -p ~/.agents/skills
cp -r <repo>/skills/* ~/.agents/skills/
```

`.agents/skills/` es la convención cross-tool del estándar Agent Skills. Codex y Gemini CLI la leen directamente.

---

### Cursor

Cursor no usa el formato Agent Skills, sino reglas en `.cursor/rules/*.mdc`. Como adaptación:

1. Crea `.cursor/rules/` en tu proyecto.
2. Por cada skill que quieras activar, crea un archivo `.mdc` con este formato:

```markdown
---
description: <copia el description del frontmatter del SKILL.md>
alwaysApply: false
---

<copia el cuerpo del SKILL.md>
```

Con `description` (y sin `globs` ni `alwaysApply: true`), Cursor aplicará la regla cuando el agente la considere relevante — comportamiento equivalente al routing por descripción de Agent Skills.

Para la guía orquestadora, pon `alwaysApply: true` en `playbook-guia.mdc` si quieres que esté siempre presente.

---

### GitHub Copilot

Copilot soporta un único archivo `.github/copilot-instructions.md` por repo, sin routing por descripción. Recomendaciones:

- **Equipo trabajando solo con este playbook:** concatena los `SKILL.md` que vayáis a usar más en `.github/copilot-instructions.md`.
- **Skill puntual:** pega el contenido del `SKILL.md` concreto en el chat de Copilot al empezar la tarea.

---

### Windsurf · Cline · Continue · otros

Para cualquier harness sin soporte modular nativo:

1. Identifica la skill que necesites (`skills/<nombre>/SKILL.md`).
2. Copia su contenido en el archivo de instrucciones del harness (`.windsurfrules`, `.clinerules`, instrucciones del proyecto, etc.).
3. Si vas a usar varias, empieza con [`playbook-guia/SKILL.md`](skills/playbook-guia/SKILL.md) para tener el mapa de fases siempre disponible.

---

### Tabla resumen de rutas

| Harness | Ruta usuario | Ruta workspace | Soporte nativo |
|---|---|---|---|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` | ✅ Agent Skills |
| Claude Desktop / claude.ai | — | (pegar en proyecto) | Manual |
| OpenAI Codex CLI | `~/.agents/skills/` | `.agents/skills/` | ✅ Agent Skills |
| Google Gemini CLI | `~/.gemini/skills/` o `~/.agents/skills/` | `.gemini/skills/` o `.agents/skills/` | ✅ Agent Skills |
| Cursor | — | `.cursor/rules/*.mdc` | Adaptación |
| GitHub Copilot | — | `.github/copilot-instructions.md` | Adaptación |
| Windsurf / Cline / Continue | — | `.windsurfrules` / `.clinerules` / etc. | Adaptación |

## Cómo funciona

Cada skill es un fichero `SKILL.md` con frontmatter (`name`, `description`) que Claude carga bajo demanda. La descripción se evalúa contra el mensaje del usuario: si menciona alguna de las frases de activación (en castellano), la skill se activa automáticamente.

Si no sabes qué habilidad usar, invoca **`playbook-guia`** y te orienta según la fase del proceso en la que te encuentres.

## Skills disponibles

### 🧭 Orquestador

| Skill | Para qué sirve |
|---|---|
| **`playbook-guia`** | Recomienda la habilidad correcta según la fase del proceso y sugiere el siguiente paso. |

**Úsala cuando digas:** "por dónde empiezo", "qué habilidad uso ahora", "en qué fase estoy", "cuál es el siguiente paso".

---

### 01 · Descubrir y empatizar

Entender el reto, el sistema y las señales antes de decidir nada.

| Skill | Habilidad |
|---|---|
| `descubrir-comprender-contexto-y-reto` | Primera lectura del reto y su contexto estratégico (sin proponer soluciones todavía). |
| `descubrir-explorar-como-funciona-el-servicio` | Exploración abierta del sistema: actores, canales, procesos, handoffs, frontstage/backstage y puntos ciegos. |
| `descubrir-investigar-y-capturar-evidencias` | Recogida y selección de señales cualitativas, cuantitativas y operativas, trazables y con contexto. |
| `descubrir-detectar-patrones-iniciales` | Agrupación de evidencias y detección de temas recurrentes, tensiones, contradicciones y excepciones — con nivel de confianza. |

**Úsalas cuando digas:** "entender el reto", "explorar cómo funciona el servicio", "capturar evidencias", "detectar patrones", "agrupar señales", "abrir la mirada de sistema".

---

### 02 · Definir y sintetizar

Convertir señales en aprendizajes, modelar el servicio y formular el reto con impacto.

| Skill | Habilidad |
|---|---|
| `definir-sintetizar-evidencias-y-aprendizajes` | Convertir evidencias y patrones en aprendizajes accionables, con sesgos, áreas inexploradas y decisión que activa. |
| `definir-construir-lectura-sistemica-de-los-aprendizajes` | Lectura sistémica que conecta experiencia, backstage, actores, procesos e impacto para que emerjan retos y decisiones. |
| `definir-modelar-el-servicio-para-explicar-el-diagnostico` | Modelo intencionado del servicio (journey, blueprint) con momentos de la verdad, factores higiénicos/motivacionales, generadores de expectativas y handoffs. |
| `definir-formular-retos-con-impacto-idg` | Ficha de reto en formato Impact-Driven Growth™ (Negocio · Reto · Cambio esperado) lista para copiar a la herramienta IDG. |

**Úsalas cuando digas:** "sintetizar evidencias", "qué hemos aprendido", "lectura sistémica", "modelar el servicio para el diagnóstico", "formular el reto con IDG".

---

### 03 · Idear y formular apuestas

Generar, seleccionar, esbozar y convertir iniciativas en hipótesis priorizadas.

| Skill | Habilidad |
|---|---|
| `idear-generar-iniciativas` | Abanico de iniciativas de distinto tamaño (ajuste puntual → cambio sistémico), sin filtrar todavía. |
| `idear-converger-y-seleccionar-iniciativas` | Pocas iniciativas prometedoras y diversas, con listado limpio final como acciones concretas. |
| `idear-esbozar-el-escenario-to-be-de-una-iniciativa` | Esbozo provisional de cómo cambiaría el servicio si la iniciativa funcionase — frontstage, backstage, expectativas, dependencias. |
| `idear-formular-hipotesis` | Hipótesis causales testeables con la lógica "Creemos que si X, provocará Y, lo que moverá Z". |
| `idear-priorizar-hipotesis-riesgo-valor` | Priorización por 4 cuadrantes (Implementar y medir · Experimentar · Aparcar · Descartar) con recomendación de foco. |

**Úsalas cuando digas:** "generar iniciativas", "seleccionar iniciativas", "esbozar el to-be", "formular hipótesis", "priorizar hipótesis", "matriz riesgo-valor".

---

### 04 · Validar, medir e iterar

Identificar la incógnita crítica, aprender con la mínima inversión, decidir y medir impacto.

| Skill | Habilidad |
|---|---|
| `validar-identificar-la-incognita-critica` | El "talón de Aquiles" de la hipótesis convertido en pregunta de aprendizaje accionable. |
| `validar-disenar-experimentos` | Tres opciones de experimento (rápido · ligero · robusto) con qué aprender, cómo probar, qué observar y qué decisión permite. |
| `validar-sintetizar-aprendizaje-y-decidir` | Aprendizaje clave, resultado vs criterio y decisión recomendada (avanzar/ajustar/repetir/descartar/pausar/repriorizar). |
| `validar-medir-y-hacer-seguimiento-de-metricas` | Plan de seguimiento conectado a aprendizaje y decisión: señal, fuente, frecuencia, criterio de lectura y riesgo de mala interpretación. |

**Úsalas cuando digas:** "identificar la incógnita crítica", "diseñar experimento", "qué aprendimos del test", "decidir tras la validación", "plan de medición", "métricas vanity".

---

## Flujos típicos

| Punto de partida | Recorrido sugerido |
|---|---|
| Reto nuevo desde cero | 0101 → 0102 → 0103 → 0104 → 0201 → 0202 → 0203 → 0204 → 0301 → 0302 → 0303 → 0304 → 0305 → 0401 → 0402 → 0403 → 0404 |
| Tengo research disperso | 0103 → 0104 → 0201 → 0202 |
| Reto definido, necesito ideas | 0301 → 0302 → 0303 → 0304 → 0305 |
| Tengo hipótesis, quiero validar | 0401 → 0402 → 0403 |
| Ya lanzamos algo, leemos métricas | 0404 → 0403 |

## Principios transversales

- **Guardarraíles IDG™**: antes de cerrar cualquier habilidad, revisa sistema, valor, decisión, aprendizaje, criterio IA y momento del proceso.
- **No saltarse fases**: si una habilidad pide entradas que no existen, retroceder.
- **IA como compañera cognitiva**, no como oráculo: cuestionar siempre lo generado.
- **Iteración**: volver a fases anteriores es aprendizaje, no fallo.

## Estructura de cada skill

```
skills/
  <nombre-skill>/
    SKILL.md   # Frontmatter (name + description) + cuerpo de la habilidad
```

El cuerpo sigue siempre la misma plantilla:

- **Instrucción** — qué hace la habilidad
- **Mentalidad activa** — qué pensamiento debe sostenerla
- **Entrada mínima** — qué se necesita para activarla
- **Información que puede ayudar** — opcionales que enriquecen el resultado
- **Salida esperada** — estructura del entregable
- **Guardarraíles IDG™** — checks de cierre
- **Plantillas relacionadas** — fichas del playbook a las que se conecta

## Fuente y plantillas

Estas skills derivan del **AI Innovation Playbook** completo (Service Design + Impact-Driven Growth™), que incluye también:

- Fases de trabajo
- Plantillas de servicio (mapa de servicio, journey, blueprint, ficha de reto, iniciativa, hipótesis, experimento, decisión, plan de medición, matriz riesgo-valor, etc.)
- Guardarraíles IDG™

Las habilidades canónicas viven en el playbook web (`habilidades/` dentro de la documentación). El cuerpo de cada `SKILL.md` de este repo se mantiene alineado con la ficha canónica de la habilidad.

## Contribuir

Las skills siguen la convención de [Agent Skills](https://agentskills.io/) y son compatibles con [skills.sh](https://skills.sh). Para añadir o modificar una skill:

1. Edita el `SKILL.md` correspondiente en `skills/<nombre>/`.
2. Asegúrate de que el frontmatter (`name` + `description`) describe con frases de activación claras cuándo debe activarse.
3. Mantén el cuerpo siguiendo la plantilla común.

## Licencia

MIT
