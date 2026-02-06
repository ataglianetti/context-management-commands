# Context Management Commands

Custom slash commands for Claude Code, designed for Product Managers using Obsidian as a knowledge management system.

## What This Is

These are prompt files that extend Claude Code with domain-specific workflows. Each `.md` file defines a slash command (e.g., `/daily-note`, `/research`) that Claude executes within your vault context.

## Commands

| Command | Description |
|---------|-------------|
| `/daily-note` | Generate daily note log from vault changes and git commits |
| `/draft-reply` | Draft reply to a Thread note (email/Slack/Teams) |
| `/f20-review` | Prep bullets for weekly F20 Product & PM Sync |
| `/first-light` | Morning journal entry with dictation cleanup |
| `/idea-board` | Weekly initiative updates for JIRA Idea Board |
| `/last-light` | Evening journal entry with dictation cleanup |
| `/meeting-notes` | Format rough meeting notes into structured note |
| `/product-sentiment` | Product sentiment tracking |
| `/project-status` | Generate weekly status update for all projects |
| `/refresh` | Re-onboarding interview to refresh Claude context |
| `/research` | Deep research with web search, capture to vault |
| `/resource` | Process article/video into summarized note |
| `/review` | Weekly review of active work items |
| `/save-resource` | Process article/video into summarized note |
| `/save-thread` | Save email/Slack/Teams thread as Thread note |
| `/timesheet` | Review time allocation for previous month |
| `/update-memory` | Update memory file with session context |
| `/update-thread` | Add new replies to existing Thread note |

## Setup

1. Place these files in your Claude Code commands directory:
   ```
   .claude/commands/
   ```

2. Commands become available as `/command-name` in Claude Code sessions.

## How Commands Work

Each command file contains:
- **Frontmatter**: `description` field shown in command picker
- **Body**: Detailed instructions Claude follows when the command runs

Commands can reference:
- Vault structure and templates
- Frontmatter conventions
- File organization patterns
- External tools (git, web search, MCP servers)

## Customization

These commands assume a specific vault structure (Contexts/, Calendar/, Resources/Templates/). Adapt paths and patterns to match your setup.

Key assumptions:
- Daily notes at `Calendar/YYYY-MM-DD.md`
- Templates in `Resources/Templates/`
- Context-based organization under `Contexts/`
- Git-tracked content folders

## License

MIT
