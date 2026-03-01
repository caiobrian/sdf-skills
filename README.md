# SDF — Spec-Driven Flow

Framework de desenvolvimento estruturado para Claude Code. Organiza o trabalho em fases: **Discovery → Spec → Build → Verify → Document**.

## Instalação

### Via `npx skills` (recomendado)

```bash
# Instalar globalmente (disponível em todos os projetos)
npx skills add caiobrian/sdf-skills --global --agent claude-code

# Ou instalar apenas no projeto atual
npx skills add caiobrian/sdf-skills --agent claude-code
```

### Manual

```bash
# Global
git clone https://github.com/caiobrian/sdf-skills.git /tmp/sdf-skills
cp -r /tmp/sdf-skills/skills/sdf ~/.claude/skills/sdf
cp -r /tmp/sdf-skills/skills/sdf-setup ~/.claude/skills/sdf-setup
rm -rf /tmp/sdf-skills

# Projeto local
git clone https://github.com/caiobrian/sdf-skills.git /tmp/sdf-skills
cp -r /tmp/sdf-skills/skills/sdf .claude/skills/sdf
cp -r /tmp/sdf-skills/skills/sdf-setup .claude/skills/sdf-setup
rm -rf /tmp/sdf-skills
```

## Skills incluídos

### `sdf-setup`
Inicializa a constituição do projeto (`.claude/CLAUDE.md` e `LessonsLearned.md`). Roda uma vez por projeto.

**Triggers:** `setup sdf`, `iniciar projeto`, `configurar sdf`, `/sdf-setup`

### `sdf`
Workflow principal. Router inteligente que detecta a fase e executa:

| Fase | Quando | Contexto |
|------|--------|----------|
| **Quick Track** | Bug fix, UI tweak, config | Main context |
| **Discovery** | Problema novo, sem spec | Main context |
| **Spec** | Problem statement existe | Main context |
| **Build** | Spec aprovada, tasks pendentes | Subagent por task |
| **Verify** | Code pronto, precisa validar | Subagent |
| **Document** | Tudo pronto, fechar ciclo | Main context |

**Triggers:** `sdf`, `nova feature`, `novo problema`, `gerar spec`, `implementar`, `validar`, `documentar`, `fix rápido`, `/sdf`

## Fluxo completo

```
/sdf-setup          → Constituição do projeto (uma vez)
  ↓
Discovery           → Entender o problema
  ↓
Spec                → requirements.md → plan.md → tasks.md
  ↓
Build               → Implementar (1 subagent por task)
  ↓
Verify              → Testar contra spec (subagent)
  ↓
Document            → Fechar ciclo + PR description
```

## Estrutura de artefatos gerados

```
specs/
└── <feature-name>/
    ├── requirements.md    # RF-xx, RNF-xx, EC-xx, CA-xx
    ├── plan.md            # Types, interfaces, strategy
    └── tasks.md           # T-xx ordered by dependency
```

## Princípios

- **Spec é contrato** — Build e Verify seguem a spec, não inventam
- **Subagents** — Build e Verify rodam em contexto fresco (evita context rot)
- **Progressive disclosure** — SKILL.md é router, detalhes nas fases
- **Quick Track** — Atalho para tarefas pequenas, escala se crescer

## Licença

MIT
