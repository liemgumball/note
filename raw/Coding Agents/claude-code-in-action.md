---
Link: "[Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action)"
---
## Overview

**Claude Code in Action** is an official *Anthropic* course that teaches you how to use Claude Code effectively for real-world software development tasks. The course covers how to leverage Claude Code's agentic capabilities — from writing and editing code to navigating codebases, running commands, and managing complex workflows directly from the terminal.

**What you'll learn:**
- How to get started with Claude Code
- Core features: file editing, codebase navigation, running tests and commands
- Advanced modes like Planning and Thinking
- Best practices for agentic coding workflows

---

## Lesson: Planning vs Thinking

**Lesson Link:** [Planning and Thinking](https://anthropic.skilljar.com/claude-code-in-action/303236)

This lesson explains two distinct modes in Claude Code that help you tackle complex tasks more effectively.

| | **Planning Mode** | **Thinking Mode** |
|---|---|---|
| **What it is** | Claude creates a step-by-step plan before taking action | Claude reasons deeply through a problem before answering |
| **How to activate** | `/plan` command or shift+tab | `--think` flag (e.g. `--think` or `--think-hard`) |
| **When to use** | Multi-step tasks where you want to review and approve steps first | Hard problems that need deeper reasoning or analysis |
| **Claude takes action?** | No — pauses for your approval before doing anything | Yes — acts after reasoning, no approval step |
| **Best for** | Refactoring, large features, risky changes | Debugging tricky bugs, architecture decisions, complex logic |
| **Output** | A proposed plan you can edit or approve | A response with visible reasoning ("thinking") included |

---

## Conversation Management

### Rewinding Conversations

**Purpose:** Go back to an earlier point in the conversation and branch off in a different direction, discarding everything after that point.

**Benefits:**
- Undo a bad or unwanted chain of edits without manually reverting files
- Try a different approach from a known-good checkpoint
- Recover from mistakes without starting the whole session over

**How to use:** Press `Esc` to access the conversation history, then select the message you want to rewind to.

---

### `/compact` Command

**Purpose:** Summarize the current conversation into a condensed context, freeing up space in the context window while retaining the important information.

**Benefits:**
- Keeps long sessions running smoothly without hitting context limits
- Preserves key decisions, file changes, and task progress
- Lets you continue working without losing important context

**How to use:** Type `/compact` at any point in the conversation.

---

### `/clear` Command

**Purpose:** Completely wipe the current conversation context and start fresh.

**Benefits:**
- Gives Claude a clean slate — no leftover context from previous tasks that could cause confusion
- Useful when switching to a completely unrelated task in the same session
- Reduces noise and keeps responses focused

**How to use:** Type `/clear` to reset the conversation. Unlike `/compact`, nothing is retained.

---

## Custom Commands

**Purpose:** Create reusable, project-specific slash commands (e.g. `/review`, `/deploy`, `/test`) that encode your own workflows and instructions. Instead of typing the same long prompt repeatedly, you run a short command.

**Benefits:**
- Save time by turning repetitive prompts into one-word commands
- Standardize workflows across a team (everyone uses the same process)
- Commands can include dynamic arguments, making them flexible
- Stored in your repo, so they're versioned alongside your code

**How to create:**
1. Create a Markdown file inside `.claude/commands/` in your project, e.g. `.claude/commands/review.md`
2. Write your prompt/instructions inside the file — this is what Claude will run when the command is invoked
3. Use `$ARGUMENTS` in the file if you want to pass dynamic input (e.g. a filename or ticket number)
4. Run it with `/review` (or whatever you named the file)

**Example** — `.claude/commands/review.md`:
```
Review the following file for code quality, bugs, and style issues: $ARGUMENTS
Provide a brief summary with specific suggestions.
```
Then run: `/review src/auth.ts`

> 💡 **Tip:** Use the `/command-development` skill to help design and scaffold new commands. It guides you through defining the purpose, structure, and prompt content of a command effectively.

---

## Managing Permissions

**Purpose:** Control what actions Claude Code is allowed to take automatically versus what requires your explicit approval — keeping you in control of sensitive operations like file writes, shell commands, and web fetches.

**Benefits:**
- Prevents Claude from making unintended or destructive changes without asking
- Lets you move faster by pre-approving safe, repetitive actions
- Gives you fine-grained control per tool or action type

**How it works:**

| Permission Level | What it means |
|---|---|
| **Ask every time** (default) | Claude pauses and asks before running the action |
| **Allow for this session** | Claude can run this action freely for the rest of the session |
| **Always allow** | Permanently approved — stored in settings, no prompt in future sessions |
| **Deny** | Claude is blocked from using this action entirely |

**Tips:**
- When Claude asks for permission, you can choose to allow it once or always — pick "always" only for truly safe, routine actions
- You can review and reset permissions in Claude Code settings at any time
- Use restrictive permissions in unfamiliar codebases to stay safe

**`settings.local.json` example:**

Stored at `.claude/settings.local.json` (gitignored, local to your machine). This is where "always allow" choices get saved automatically, but you can also edit it manually.

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run test:*)",
      "Bash(git diff:*)",
      "Bash(git log:*)",
      "ReadFile",
      "WriteFile"
    ],
    "deny": [
      "Bash(rm -rf:*)",
      "Bash(git push:*)"
    ]
  }
}
```

> Each entry in `allow`/`deny` maps to a tool name or a shell command pattern. Wildcards (`*`) let you approve a family of commands (e.g. all `npm run test:*` variants) without approving everything.

---

## Prompting Tips

### Structure your prompts with a goal + steps

A simple and effective pattern for complex tasks:

```
Your goal is to [clear objective].

Here is how you can do it:
1. [First step]
2. [Second step]
3. [Third step]
```

**Why it works:**
- The goal line anchors Claude to the desired outcome — reducing drift on long tasks
- Numbered steps give Claude an explicit plan to follow, reducing guesswork
- This structure mirrors how Claude's own planning mode thinks, so it aligns naturally with how Claude reasons

**Example:**
```
Your goal is to refactor the authentication module to use JWTs.

Here is how you can do it:
1. Read the current auth implementation in src/auth/
2. Identify all session-based logic and note what needs to change
3. Replace session handling with JWT generation and validation
4. Update any middleware or routes that depend on the old auth
5. Run the test suite and fix any failures
```

---

## GitHub Integration — Behind the Scenes

> 📊 See the full visual: [github-integration-flow.html](github-integration-flow.html)
> 🔷 Sequence diagram: [github-integration-flow.mermaid](github-integration-flow.mermaid)

![[github-integration-flow.excalidraw]]
### How it works (step by step)

1. **User creates a GitHub Issue** and tags `@claude` in the body
2. **GitHub fires an `issues` webhook** → triggers the Actions workflow (`.github/workflows/claude.yml`)
3. **GitHub spins up a Runner VM** — a temporary Ubuntu VM on GitHub's cloud servers
4. **Runner checks out the repo** into its filesystem
5. **Claude Code is invoked inside the Runner** with the issue text as its prompt, authenticated via `ANTHROPIC_API_KEY`
6. **Claude reads the codebase** using its tools (ReadFile, Grep, Glob) to understand the code
7. **Claude makes code changes** directly on the Runner's filesystem
8. **Tests run inside the Runner VM** — `npm test`, `pytest`, etc. run in the same VM shell
9. **Claude opens a Pull Request** via the GitHub API using `GITHUB_TOKEN`
10. **Developer reviews and merges** the PR

### Q: Where does the app run when `@claude` tests it?

Inside the **GitHub Actions Runner** — a temporary, ephemeral Ubuntu VM hosted on **GitHub's cloud infrastructure**. It is not running on your local machine or on Anthropic's servers. The VM is destroyed after the job finishes.

### Q: How does the Action trigger when a user creates an issue?

The workflow file listens for the `issues` event:

```yaml
on:
  issues:
    types: [opened]
```

When the issue is created → GitHub fires the event → Runner VM spins up → Claude Code runs with the issue as its prompt → it autonomously fixes the code and opens a PR.

**Required secrets:**
- `ANTHROPIC_API_KEY` — authenticates Claude Code
- `GITHUB_TOKEN` — lets Claude push branches and open PRs (auto-provided by GitHub)

---

## Hooks

**What it does:** Hooks let you run your own shell commands automatically at specific points in Claude Code's lifecycle — before or after Claude takes an action. Think of them as event listeners for Claude's behaviour.
![[Pasted image 20260325215354.png]]

**Why it's useful:**
- Enforce team rules automatically (e.g. always run linter after edits)
- Log or audit what Claude does
- Block unsafe actions before they happen
- Trigger notifications or side-effects on tool use

Hooks are defined in `settings.local.json` under a `"hooks"` key.

---

### Hook Matchers

The `matcher` field targets a specific Claude Code tool by name. Each hook entry fires only when that tool is invoked.

| Matcher | Tool it targets | Common use |
|---|---|---|
| `*` | All tools (wildcard) | Global audit logging |
| `Bash` | Shell command execution | Block dangerous commands, log all shell activity |
| `ReadFile` | Reading file contents | Block access to secrets (`.env`, key files) |
| `WriteFile` | Writing/creating files | Validate content before saving, log writes |
| `Edit` | Editing existing files | Auto-format after edits, enforce style rules |
| `MultiEdit` | Multiple edits in one call | Same as Edit but for batch changes |
| `Glob` | File pattern search | Restrict which directories Claude can scan |
| `Grep` | Searching file contents | Log what Claude is searching for |
| `WebFetch` | Fetching a URL | Block external requests, log web access |
| `WebSearch` | Web search queries | Restrict or log search queries |
| `Task` | Spawning a subagent | Audit or limit parallel agent usage |
| `TodoWrite` | Writing the todo list | Log task planning |
| `NotebookEdit` | Editing Jupyter notebooks | Validate notebook cell changes |

> Matchers are **case-sensitive** and must match the exact tool name. Use `"*"` to catch every tool call in one hook.

---

### Type 1: `PreToolUse`

Runs **before** Claude executes a tool. You can use it to inspect, log, or **block** the action entirely.

If your command exits with code `2`, Claude cancels the tool call and shows your output as the reason.

**Example — block Claude from reading `.env` files:**

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "ReadFile",
        "hooks": [
          {
            "type": "command",
            "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -q '\\.env'; then echo 'Reading .env files is not allowed'; exit 2; fi"
          }
        ]
      }
    ]
  }
}
```

**Example — log every file write:**

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "WriteFile",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"[$(date)] WriteFile: $CLAUDE_TOOL_INPUT\" >> ~/claude-audit.log"
          }
        ]
      }
    ]
  }
}
```

---

### Type 2: `PostToolUse`

Runs **after** Claude finishes executing a tool. Use it to react to what Claude just did — run a formatter, notify, validate, etc.

Claude receives your command's output and can use it to decide next steps.

**Example — auto-format after every file edit:**

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "WriteFile",
        "hooks": [
          {
            "type": "command",
            "command": "prettier --write \"$(echo $CLAUDE_TOOL_RESULT | jq -r '.path')\" 2>&1"
          }
        ]
      }
    ]
  }
}
```

**Example — run tests after any Bash command:**

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "npm test --silent 2>&1 | tail -5"
          }
        ]
      }
    ]
  }
}
```

---

### Type 3: `Notification`

Runs when Claude Code sends a **notification** to the user — typically at the end of a long task or when it needs your attention. Use it to route notifications to wherever suits you (Slack, terminal bell, custom sound, etc.).

Does **not** use a `matcher` field — it fires on all notification events.

**Example — send a Slack message when Claude finishes a task:**

```json
{
  "hooks": {
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "curl -s -X POST $SLACK_WEBHOOK_URL -d \"{\\\"text\\\": \\\"Claude Code: $CLAUDE_NOTIFICATION_MESSAGE\\\"}\" > /dev/null"
          }
        ]
      }
    ]
  }
}
```

**Example — play a sound when Claude finishes:**

```json
{
  "hooks": {
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "afplay /System/Library/Sounds/Glass.aiff"
          }
        ]
      }
    ]
  }
}
```

---

### Type 4: `Stop`

Runs when Claude Code **fully stops** — after it has finished its entire response and all tool use. This is the very end of a Claude turn.

Use it for final cleanup, summary logging, or sending a "done" signal to another system.

**Example — log a completion timestamp:**

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo \"[$(date)] Claude session ended\" >> ~/claude-sessions.log"
          }
        ]
      }
    ]
  }
}
```

---

### Summary

| | `PreToolUse` | `PostToolUse` | `Notification` | `Stop` |
|---|---|---|---|---|
| **When it runs** | Before a tool is used | After a tool is used | When Claude sends a notification | When Claude fully stops |
| **Can block action?** | Yes — exit code `2` | No | No | No |
| **Uses `matcher`?** | Yes | Yes | No | No |
| **Use for** | Validation, blocking | Formatting, testing | Custom alerts, Slack, sounds | Cleanup, final logging |
| **Env variable** | `$CLAUDE_TOOL_INPUT` | `$CLAUDE_TOOL_RESULT` | `$CLAUDE_NOTIFICATION_MESSAGE` | — |
