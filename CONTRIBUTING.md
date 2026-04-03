# Contributing to SDF

Thanks for your interest in improving SDF. Contributions are welcome — bug fixes, new phase behaviors, documentation improvements, and examples.

## What SDF is (and isn't)

SDF is a set of **Claude Code skills** — plain markdown files that guide Claude's behavior. There is no runtime code, build step, or framework. A contribution is a well-crafted prompt change or a new/improved document.

## How to contribute

### Reporting bugs

Open an issue using the **Bug report** template. Describe the phase, what went wrong, and what you expected to happen.

### Suggesting changes

Open an issue using the **Feature request** template before writing anything. It's easier to discuss direction before you invest time in writing.

### Submitting a change

1. Fork the repository
2. Create a branch: `git checkout -b fix/your-description` or `feat/your-description`
3. Make your changes
4. Test manually — install the skill locally and run through the affected phases
5. Open a pull request against `main`

## Testing your changes locally

```bash
# Clone your fork
git clone https://github.com/<your-username>/sdf-skills.git /tmp/sdf-skills

# Install from local path
npx skills add /tmp/sdf-skills --global --agent claude-code --all -y

# After testing, uninstall
npx skills remove --global sdf sdf-setup
```

## Guidelines for phase files

- **Be explicit, not prescriptive** — tell Claude *what* to do at each step, not *how* to think about it
- **Keep rules at the bottom** — each phase file ends with a `## Rules` section
- **Language-agnostic** — phases must work regardless of the user's project stack
- **Short prompts > long prompts** — every sentence Claude reads costs context. Cut anything that doesn't change behavior.

## Guidelines for examples

Examples in `docs/examples/` should be realistic — based on a real feature, not a toy. They demonstrate what good `requirements.md`, `plan.md`, and `tasks.md` files look like. If you add an example, make sure all requirement IDs referenced in tasks actually appear in requirements.

## Commit messages

Use the format: `<type>: <short description>`

Types: `fix`, `feat`, `docs`, `refactor`

Examples:
- `fix: discovery phase asks too many questions at once`
- `feat: add wave grouping hint in build phase`
- `docs: add example for authentication feature`
