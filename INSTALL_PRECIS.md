# Install Precis Infrastructure

**Purpose**: Copy and adapt the Precis Claude Code infrastructure to a new or existing project.

**Usage**: From your target project, reference this file and specify what to exclude.

## Parameters

- `$ARGUMENTS` - Specify components using ONE of these formats:

### Exclude Mode (default)
```
exclude: component1,component2
```
Copies everything EXCEPT the listed components.

### Include Mode
```
include: component1,component2
```
Copies ONLY the listed components (plus `commands` and `settings` which are always included).

### Valid Component Names
`commands`, `agents`, `settings`, `hack`, `github`, `thoughts`, `agent_docs`

### Examples
| Argument | Result |
|----------|--------|
| `exclude: hack,github` | Everything except hack/ and .github/ |
| `include: commands` | Only commands (minimal install) |
| `include: commands,agents,thoughts` | Commands, agents, and thoughts structure |
| *(empty)* | Copy everything |

**Note**: `commands` and `settings` are ALWAYS copied regardless of mode.

## Source Location

The Precis infrastructure is located at: `/Users/jefferson/Projects/precis`

## Components Available for Copy

| Component | Source Path | Description |
|-----------|-------------|-------------|
| `commands` | `.claude/commands/` | Slash commands (/commit, /create_plan, etc.) **[Always copied]** |
| `settings` | `.claude/settings.json` | Claude Code permissions and settings **[Always copied]** |
| `agents` | `.claude/agents/` | Sub-agent definitions for Task tool |
| `hack` | `hack/` | Utility shell scripts (worktree, cleanup, etc.) |
| `github` | `.github/` | GitHub templates (PR template, issue templates) |
| `thoughts` | `thoughts/` | Documentation structure (plans, research, analysis) |
| `agent_docs` | `agent_docs/` | Extended documentation for agents |

## Execution Instructions

### Step 1: Parse Arguments

Parse `$ARGUMENTS` to determine which components to copy:

1. **Detect mode**:
   - If starts with `include:` → Include mode
   - If starts with `exclude:` → Exclude mode
   - If empty or not provided → Copy everything

2. **Parse component list**:
   - Extract text after `include:` or `exclude:`
   - Split by comma and trim whitespace
   - Normalize to lowercase

3. **Build copy list**:
   - **Include mode**: Start with `[commands, settings]`, add specified components
   - **Exclude mode**: Start with all components, remove specified ones
   - **Empty**: Copy all components

All valid components: `commands`, `agents`, `settings`, `hack`, `github`, `thoughts`, `agent_docs`

### Step 2: Prepare Target Project

1. **Check if `.claude/` exists** in the current working directory
   - If yes, warn the user and ask whether to merge or replace
   - If no, create the directory

2. **Check for existing files** that would be overwritten
   - List any conflicts before proceeding
   - Ask user how to handle conflicts (skip, overwrite, merge)

### Step 3: Copy Components

Copy each component unless excluded. For each component:

#### Commands (`.claude/commands/`) - Always copied
```
Source: /Users/jefferson/Projects/precis/.claude/commands/
Target: ./.claude/commands/
```
Files to copy:
- `commit.md`
- `create_plan.md`
- `create_worktree.md`
- `debug.md`
- `describe_pr.md`
- `founder_mode.md`
- `implement_plan.md`
- `init_claude_md.md`
- `linear.md`
- `local_review.md`
- `research_codebase.md`
- `validate_plan.md`

#### Agents (`.claude/agents/`) - Skip if "agents" in exclusions
```
Source: /Users/jefferson/Projects/precis/.claude/agents/
Target: ./.claude/agents/
```
Files to copy:
- `codebase-analyzer.md`
- `codebase-locator.md`
- `codebase-pattern-finder.md`
- `thoughts-analyzer.md`
- `thoughts-locator.md`
- `web-search-researcher.md`

#### Settings (`.claude/settings.json`) - Always copied
```
Source: /Users/jefferson/Projects/precis/.claude/settings.json
Target: ./.claude/settings.json
```
**Important**: If target already has settings.json, MERGE the settings intelligently (combine permissions, preserve existing project-specific settings).

#### Hack Scripts (`hack/`) - Skip if "hack" in exclusions
```
Source: /Users/jefferson/Projects/precis/hack/
Target: ./hack/
```
Files to copy:
- `cleanup_worktree.sh`
- `create_worktree.sh`
- `port-utils.sh`
- `run_silent.sh`
- `setup_repo.sh`
- `CLAUDE.md`

After copying, make scripts executable: `chmod +x hack/*.sh`

#### GitHub Templates (`.github/`) - Skip if "github" in exclusions
```
Source: /Users/jefferson/Projects/precis/.github/
Target: ./.github/
```
Files to copy:
- `pull_request_template.md`
- `ISSUE_TEMPLATE/bug_report.md`
- `ISSUE_TEMPLATE/feature_request.md`

#### Thoughts Structure (`thoughts/`) - Skip if "thoughts" in exclusions
```
Source: /Users/jefferson/Projects/precis/thoughts/
Target: ./thoughts/
```
Create directories with .gitkeep:
- `thoughts/`
- `thoughts/plans/`
- `thoughts/research/`
- `thoughts/analysis/`
- `thoughts/tickets/`

#### Agent Docs (`agent_docs/`) - Skip if "agent_docs" in exclusions
```
Source: /Users/jefferson/Projects/precis/agent_docs/
Target: ./agent_docs/
```
Create directory with .gitkeep.

### Step 4: Adapt to Target Project

After copying, make these adaptations:

1. **Update `create_worktree.md`** if the target project uses a different main branch:
   - Check `git symbolic-ref refs/remotes/origin/HEAD` or common branch names
   - Update branch references if needed

2. **Update hack scripts** paths if needed:
   - Check if scripts reference absolute paths and make them relative

3. **Check for existing CLAUDE.md**:
   - If exists, suggest adding the reference documentation table pointing to agent_docs/
   - If not exists, inform the user they can run `/init_claude_md` to create one

### Step 5: Summary Report

After completion, provide a summary:

```
## Precis Infrastructure Installed

### Components Copied:
- [x] Commands (12 files)
- [x] Agents (6 files)
- [x] Settings
- [ ] Hack scripts (excluded)
- [x] GitHub templates
- [x] Thoughts structure
- [x] Agent docs

### Next Steps:
1. Run `/init_claude_md` to create or update your CLAUDE.md
2. Review `.claude/settings.json` and adjust permissions as needed
3. Customize commands in `.claude/commands/` for your project
4. [If hack copied] Make scripts executable: `chmod +x hack/*.sh`

### Files NOT committed:
All files have been copied but NOT committed. Review the changes and commit when ready.

### Suggested Commit Message:
```
chore: add Claude Code infrastructure
```
```

## Important Rules

1. **DO NOT COMMIT** - Only copy files, never run git commit
2. **DO NOT MODIFY** existing project code - Only add/merge Precis infrastructure
3. **ASK BEFORE OVERWRITING** - If a file already exists, confirm with user
4. **PRESERVE PROJECT SETTINGS** - When merging settings.json, keep existing project configurations
5. **REPORT ALL ACTIONS** - List every file copied/created/skipped

## Example Invocations

### Copy everything
```
Install Precis infrastructure
```

### Exclude hack and github
```
Install Precis infrastructure, exclude: hack,github
```

### Include only commands and agents
```
Install Precis infrastructure, include: commands,agents
```

### Minimal install (commands only)
```
Install Precis infrastructure, include: commands
```

### Full dev setup (exclude github templates)
```
Install Precis infrastructure, exclude: github
```
