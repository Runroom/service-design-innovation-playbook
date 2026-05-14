# AGENTS.md

Guía para agentes de IA (Claude Code, Cursor, Copilot…) que trabajen en este repositorio.

## Visión general

Repositorio público de **Agent Skills** que operacionalizan un playbook de innovación en servicios con IA. Las skills cubren cuatro fases: Descubrir, Definir, Idear y Validar.

## Estructura del repositorio

```
.
├── README.md                        # Documentación pública del set de skills
├── AGENTS.md                        # Este archivo
├── skills/                          # Skills instalables (raíz pública)
│   ├── playbook-guia/               # Skill orquestadora
│   │   └── SKILL.md
│   ├── descubrir-*/                 # 4 skills de la fase 01
│   ├── definir-*/                   # 4 skills de la fase 02
│   ├── idear-*/                     # 4 skills de la fase 03
│   └── validar-*/                   # 5 skills de la fase 04
├── 02_AI Innovation Playbook/       # Material fuente del playbook
│   ├── 01_Introduccion...md
│   ├── 02_Fases de trabajo/
│   ├── 03_Habilidades/              # Habilidades originales (fuente de las skills)
│   └── 04_Plantillas/               # Plantillas del playbook
└── .claude/
    └── skills -> ../skills          # Symlink para autodescubrimiento local
```

## Convenciones para crear o modificar skills

### Nombre de la skill

`kebab-case`, con prefijo de fase para mantener el orden visual:

- `descubrir-*` para la fase 01
- `definir-*` para la fase 02
- `idear-*` para la fase 03
- `validar-*` para la fase 04

### Formato de SKILL.md

```markdown
---
name: <nombre-kebab-case>
description: Habilidad XXXX del AI Innovation Playbook. Úsala cuando el usuario pida "<frase 1>", "<frase 2>"... Resumen breve del entregable.
---

# XXXX <Título de la habilidad>

Eres una guía experta en <ámbito>. Aplica la habilidad XXXX del AI Innovation Playbook.

## Instrucción
...

## Mentalidad activa
...

## Entrada mínima que debes pedir si no la tienes
...

## Información que puede enriquecer ... (opcional)
...

## Salida esperada
...

## Guardarraíles IDG™
...

## Plantillas relacionadas
- `04_Plantillas/<plantilla>.md`
```

### Descripción y activación

La `description` del frontmatter es lo único que se carga en contexto antes de invocar la skill. Debe:

- Indicar la habilidad numérica del playbook (0101, 0102…).
- Incluir frases de activación en castellano entre comillas.
- Resumir el entregable esperado.

### Idioma

Todo el contenido va en **castellano** para mantener coherencia con el playbook fuente.

## Material fuente

Cada skill deriva de una ficha en `02_AI Innovation Playbook/03_Habilidades/`. Si se modifica una skill, la ficha fuente sirve como referencia canónica de Instrucción, Mentalidad, Entrada mínima y Salida esperada.

## Instalación end-to-end

- **Vía skills.sh:** `npx skills add <owner>/<repo>`
- **Manual Claude Code:** `cp -r skills/<nombre> ~/.claude/skills/`
- **claude.ai / Claude Desktop:** copiar contenido de `SKILL.md` al proyecto o conversación.

## Buenas prácticas de contexto

- Mantener cada `SKILL.md` enfocado y breve (< 500 líneas) — descripciones específicas mejoran el routing automático.
- No duplicar contenido entre skills; si algo es transversal, vive en `playbook-guia` o en el material del playbook.
- Las plantillas viven en `02_AI Innovation Playbook/04_Plantillas/`; las skills sólo las referencian.
