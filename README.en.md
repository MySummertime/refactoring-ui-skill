# Refactoring UI Skill

[中文说明](README.md)

This repository provides a web interface design skill for coding agents. It packages design checks as focused references, examples, and scripts so an agent can make better grounded suggestions while building, refining, or reviewing a page.

## Origin and credit

This repository is adapted from [Edison Li's refactoring-ui-skill](https://github.com/edisonmbli/refactoring-ui-skill). The original project is MIT licensed. Its copyright notice remains in [LICENSE](LICENSE). This version reorganizes the skill for use across tools and updates the installation guidance. It is maintained by [MySummertime](https://github.com/MySummertime).

The underlying design principles come from [*Refactoring UI*](https://www.refactoringui.com/) by Adam Wathan and Steve Schoger. This is an unofficial adaptation, unaffiliated with the book's authors or the original project maintainer. The book is the best place to learn the material in depth. See [ATTRIBUTION.md](ATTRIBUTION.md) for more about sources and scope.

## What it helps with

- **Build a page:** Plan content hierarchy, layout, typography, and component states before styling.
- **Refine an existing interface:** Find inconsistent spacing, weak contrast, and unclear visual priorities within the project's current design system.
- **Review a design:** Rank findings by severity and connect each recommendation to a numbered rule.
- **Create design tokens:** Establish a basic palette and token set when the project has none, including text contrast checks.
- **Explain a choice:** Retrieve the reasoning and limits behind a particular design principle.

The skill inspects the project's stack and existing tokens before suggesting changes. It works with plain CSS, Tailwind, and common component libraries without replacing the project's established conventions. When a page preview is available, review the rendered result; when only source code is available, identify visual findings as unverified.

## Install

The sole skill directory is [`.agents/skills/refactoring-ui/`](.agents/skills/refactoring-ui/). Codex and VS Code agents with project Agent Skills support can discover it when this repository is open.

To use it in another project, run these commands **from the target project's root**:

```bash
skill_checkout=$(mktemp -d)
git clone --depth 1 git@github.com:MySummertime/refactoring-ui-skill.git "$skill_checkout/repo"
mkdir -p .agents/skills
cp -R "$skill_checkout/repo/.agents/skills/refactoring-ui" .agents/skills/
rm -rf "$skill_checkout"
```

If the repository is already checked out elsewhere, adjust the source path in the last command. For a personal installation, copy the skill to `~/.agents/skills/`. Other Agent Skills hosts may use another supported directory; Claude Code, for example, uses a project's `.claude/skills/`. Keep one copy within a given scope to avoid duplicate discovery. If your agent does not discover skills automatically, adapt [`templates/AGENTS.md`](templates/AGENTS.md) to point to the installed `SKILL.md`.

## Example requests

Once installed, ask for the work in ordinary language:

> Review this settings page at mobile and desktop widths. Prioritize issues with hierarchy, spacing, and contrast, and cite the relevant rules.

> This project has no design tokens yet. Inspect the existing styles, then suggest a starter set that fits the current stack.

> Improve this empty state while keeping the project's components and color conventions.

A review should distinguish what can be verified from source from what requires seeing the page. Mention intentional design choices in your request so the agent treats them as project requirements.

## Repository map

| Path | Purpose |
| --- | --- |
| [`.agents/skills/refactoring-ui/SKILL.md`](.agents/skills/refactoring-ui/SKILL.md) | Task routing and core workflows |
| [`.agents/skills/refactoring-ui/references/`](.agents/skills/refactoring-ui/references/) | Topic-specific design guidance and review criteria |
| [`.agents/skills/refactoring-ui/scripts/`](.agents/skills/refactoring-ui/scripts/) | Palette generation, contrast checks, and token output |
| [`.agents/skills/refactoring-ui/assets/`](.agents/skills/refactoring-ui/assets/) | Reusable templates |
| [`eval/`](eval/) | Evaluation cases and scoring tools |

The skill uses Markdown and Python 3.9+ scripts and has no third-party Python dependencies. Skill discovery varies by tool version; consult your host's current documentation if it does not appear.

## License

This repository follows the [MIT License](LICENSE). See [Origin and credit](#origin-and-credit) and [ATTRIBUTION.md](ATTRIBUTION.md) for its relationship to the upstream project and the book.
