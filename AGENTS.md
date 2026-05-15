# AGENTS.md

Guía para agentes de IA (Claude Code, Cursor, Copilot…) que trabajen en este repositorio.

## Visión general

Repositorio público de **Agent Skills** que operacionalizan un playbook de innovación en servicios con IA. Las skills cubren cuatro fases: Descubrir, Definir, Idear y Validar.

## Estructura del repositorio

```
.
├── README.md                        # Documentación pública del set de skills
├── AGENTS.md                        # Este archivo
├── skills/                          # 18 skills instalables (raíz pública)
│   ├── playbook-guia/               # Skill orquestadora
│   │   └── SKILL.md
│   ├── descubrir-*/                 # 4 skills de la fase 01 (0101–0104)
│   ├── definir-*/                   # 4 skills de la fase 02 (0201–0204)
│   ├── idear-*/                     # 5 skills de la fase 03 (0301–0305)
│   └── validar-*/                   # 4 skills de la fase 04 (0401–0404)
└── .claude/
    └── skills -> ../skills          # Symlink para autodescubrimiento local
```

**Material fuente canónico:** las habilidades originales viven en el repositorio `InnovationPlaybook-web` (carpeta `site/src/content/docs/habilidades/`). Cada `SKILL.md` de este repo deriva de su ficha canónica correspondiente.

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
description: Habilidad XXXX del AI Innovation Playbook (fase <fase>). Úsala cuando el usuario pida "<frase 1>", "<frase 2>"... Resumen breve del entregable.
---

# <Título de la habilidad>

## Instrucción
...

## Mentalidad activa
...

## Guardarraíles IDG™
...

## Entrada mínima
...

## Información que puede ayudar (opcional)
...

## Salida esperada
...

## Recursos relacionados
- <Plantilla>
```

### Descripción y activación

La `description` del frontmatter es lo único que se carga en contexto antes de invocar la skill. Debe:

- Indicar la habilidad numérica del playbook (0101, 0102…) y la fase.
- Incluir frases de activación en castellano entre comillas.
- Resumir el entregable esperado.

### Idioma

Todo el contenido va en **castellano** para mantener coherencia con el playbook fuente.

## Instalación end-to-end

- **Vía skills.sh:** `npx skills add <owner>/<repo>`
- **Manual Claude Code:** `cp -r skills/<nombre> ~/.claude/skills/`
- **claude.ai / Claude Desktop:** copiar contenido de `SKILL.md` al proyecto o conversación.

## Buenas prácticas de contexto

- Mantener cada `SKILL.md` enfocado y breve (< 500 líneas) — descripciones específicas mejoran el routing automático.
- No duplicar contenido entre skills; si algo es transversal, vive en `playbook-guia` o en el material del playbook.
- Las plantillas viven en el playbook canónico (carpeta `plantillas/`); las skills sólo las referencian por nombre.
