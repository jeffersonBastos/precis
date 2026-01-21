# CLAUDE.md

## What This Project Is

Precis - A Claude Code boilerplate template providing pre-configured commands, agents, and workflows for AI-assisted development.

**Tech**: Bash, Markdown, Claude Code

## Architecture

```
precis/
├── .claude/           # Claude Code configuration
│   ├── commands/      # Slash commands (/create_plan, /commit, etc.)
│   ├── agents/        # Sub-agent definitions
│   └── settings.json  # Permissions and settings
├── .github/           # GitHub templates
│   ├── ISSUE_TEMPLATE/
│   └── pull_request_template.md
├── hack/              # Utility scripts
└── thoughts/          # Project documentation (plans, research)
```

**Key paths**:
- `.claude/commands/` - Slash command definitions
- `.claude/agents/` - Sub-agent configurations
- `hack/` - Development utility scripts

## How to Verify Changes

```bash
# Check markdown syntax
find . -name "*.md" -exec cat {} \; | head

# Test scripts
./hack/setup_repo.sh --help
```

## Reference Documentation

Read these files when relevant to your task:

| File | When to read |
|------|--------------|
| `hack/CLAUDE.md` | Working with utility scripts |
| `.claude/commands/*.md` | Modifying or understanding commands |

## Working Conventions

- All commands should be generic and project-agnostic
- Use progressive disclosure - reference separate docs instead of embedding
- Follow HumanLayer best practices for CLAUDE.md files
