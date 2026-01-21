# Precis - Claude Code Boilerplate

A comprehensive template for Claude Code projects with pre-configured commands, agents, and workflows.

## What's Included

### `.claude/` Directory

Pre-configured Claude Code commands and agents:

**Commands:**
- `/init_claude_md` - Initialize CLAUDE.md files following best practices
- `/create_plan` - Create detailed implementation plans
- `/implement_plan` - Execute implementation plans
- `/validate_plan` - Validate existing plans
- `/commit` - Commit changes with proper formatting
- `/describe_pr` - Generate PR descriptions
- `/linear` - Linear ticket management
- `/create_worktree` - Create git worktrees for isolated development
- `/research_codebase` - Research and document codebase
- `/local_review` - Local code review
- `/debug` - Debug issues during development
- `/founder_mode` - Retroactive process setup

**Agents:**
- `codebase-locator` - Find files by patterns
- `codebase-analyzer` - Understand implementation details
- `codebase-pattern-finder` - Find similar implementations
- `thoughts-locator` - Discover relevant documents
- `thoughts-analyzer` - Extract insights from documents
- `web-search-researcher` - Web research capabilities

### `.github/` Directory

GitHub templates:
- Pull request template
- Bug report issue template
- Feature request issue template

### `hack/` Directory

Utility scripts:
- `setup_repo.sh` - Initialize a new project
- `create_worktree.sh` - Create git worktrees
- `cleanup_worktree.sh` - Clean up worktrees
- `run_silent.sh` - Run commands silently
- `port-utils.sh` - Port management utilities

### `thoughts/` Directory Structure

Recommended structure for project documentation:
- `thoughts/plans/` - Implementation plans
- `thoughts/research/` - Research documents
- `thoughts/analysis/` - Analysis documents
- `thoughts/tickets/` - Ticket descriptions

## Quick Start

### Option 1: Clone and Setup

```bash
# Clone the template
git clone https://github.com/JeffersonBastos/precis.git my-project
cd my-project

# Remove template git history
rm -rf .git
git init

# Run setup
./hack/setup_repo.sh

# Customize CLAUDE.md
# Run /init_claude_md in Claude Code to customize further
```

### Option 2: Add to Existing Project

```bash
# From your existing project root
git clone https://github.com/JeffersonBastos/precis.git /tmp/precis

# Copy the folders you need
cp -r /tmp/precis/.claude .
cp -r /tmp/precis/.github .
cp -r /tmp/precis/hack .

# Create thoughts structure
mkdir -p thoughts/{plans,research,analysis,tickets}

# Clean up
rm -rf /tmp/precis

# Then in Claude Code, run:
# /init_claude_md
```

### Option 3: Cherry-pick What You Need

If you only want specific parts:

```bash
# Just the commands and agents
cp -r /path/to/precis/.claude .

# Just GitHub templates
cp -r /path/to/precis/.github .

# Just utility scripts
cp -r /path/to/precis/hack .
```

After copying, customize for your project:

1. Run `/init_claude_md` in Claude Code
2. Select option 4: "Customize the .claude commands for this project"
3. Update verification commands to match your project (`npm test`, `make check`, etc.)

## Customization

After setting up, customize for your project:

1. **CLAUDE.md** - Run `/init_claude_md` to create a project-specific CLAUDE.md
2. **Commands** - Update `.claude/commands/` with project-specific patterns
3. **Linear** - Add your team IDs to `.claude/commands/linear.md`
4. **Verification** - Update test/lint commands in plans

## Best Practices

Based on [HumanLayer's research](https://www.humanlayer.dev/blog/writing-a-good-claude-md):

1. **Keep CLAUDE.md concise** - Under 100 lines for simple projects
2. **Progressive disclosure** - Use `agent_docs/` for detailed documentation
3. **No lint rules** - Use actual linters, not CLAUDE.md instructions
4. **Universal instructions only** - Avoid task-specific hotfixes

## License

MIT
