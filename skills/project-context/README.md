# Project Context

Project Context is an agent skill and Claude plugin designed to read and maintain three durable context files: `OVERVIEW.md`, `MEMORY.md`, and `ERRORS.md`.

All three files live in `/DOCS`. Together, they stop agents from having the same conversation twice.

## Why I made it

Coding agents suffer from amnesia.

Every time you open a fresh terminal or switch models, the new agent starts with zero memory of what happened before. It can inspect your code, but it cannot see why the code looks that way.

Without durable records, the incoming agent often:

- Re-proposes an architecture you already tested and rejected last Tuesday.
- Undoes a subtle bug fix because the code looked unusual or non-standard.
- Asks you to re-explain the core data flow or tech stack from scratch.
- Dumps 200 lines of routine commit notes into documentation, burying real lessons under changelog noise.

I built `project-context` to give projects a durable, lightweight memory. It provides a structured convention for recording current architecture, hard architectural forks, and painful troubleshooting traps. Most importantly, it gives agents strict rules on what **not** to write, keeping documentation short enough to actually trust.

## The Three Durable Files

The skill organizes project knowledge into three distinct files inside `/DOCS`:

| File | Question it answers | Tense | Qualification bar |
|---|---|---|---|
| `OVERVIEW.md` | How does this project work right now? | Present | Did this change make something the file currently says untrue or incomplete? |
| `MEMORY.md` | Why is it built this way, and what did we turn down? | Past, dated (`YYYY-MM-DD`) | Would a competent contributor, seeing only the code, plausibly change this back without knowing what it cost? |
| `ERRORS.md` | What already failed, and what worked instead? | Past, dated (`YYYY-MM-DD`) | Would this waste more than an hour of someone's time again? |

Root files stay clean: `README.md` and `CHANGELOG.md` remain at your repository root. All other durable project context stays in `/DOCS`.

## How the System Works

This skill consists of two halves working together: your project rules and the agent skill.

```text
skills/project-context/
├── AGENTS_template.md     User template for project root rules
├── SKILL.md               Agent instructions for reading and writing context
├── skill.json             Skill manifest metadata
├── .claude-plugin/        Claude Code plugin manifest
├── references/            Detailed guidance on each file type and quality bars
│   ├── overview.md
│   ├── memory.md
│   ├── errors.md
│   └── examples.md
└── templates/             Starter files to bootstrap a new repository
    ├── OVERVIEW.md
    ├── MEMORY.md
    └── ERRORS.md
```

### 1. User Setup (`AGENTS_template.md`)

You start by copying `AGENTS_template.md` into your repository root as `AGENTS.md` (or into `.agents/rules/` or your tool's instructions file).

Fill in your project details, design preferences, communication tone, and boundaries. The template instructs visiting agents to:

- Consult `/DOCS/OVERVIEW.md`, `/DOCS/MEMORY.md`, and `/DOCS/ERRORS.md` before changing existing code or proposing alternative designs.
- Flag any conflict between proposed work and past decisions before touching files.
- Keep documentation up to date when architecture or behavior changes.

### 2. Agent Skill (`SKILL.md`)

When an agent runs this skill, it follows strict read and write workflows:

- **Read Phase (Grep first):** The agent reads `OVERVIEW.md` to learn the system map, then uses `grep` on headings in `MEMORY.md` and `ERRORS.md` to find relevant sections. It never dumps hundreds of lines of irrelevant history into the context window.
- **Decision Integrity:** If the task asks for an approach that `MEMORY.md` previously turned down, the agent stops and explains the recorded decision. It never quietly reverses a logged decision without explicit confirmation.
- **Write Phase (Strict filtering):** At the end of a task, the agent asks the qualification bar questions. If an edit is just routine implementation, a ten-minute bug fix, or a changelog line, the agent writes nothing.
- **Accurate Dates:** The agent runs `date` on your system before writing any dated entry, avoiding hallucinated timestamps.

## Entry Formats

The skill enforces consistent, greppable Markdown entries.

### MEMORY.md

```markdown
### Decision: <short imperative statement of what was decided>

What was decided: <one or two sentences, specific, naming real files or routes>

Why: <the reason that would otherwise be lost>

Rejected: <the alternative, and what was wrong with it>
```

### ERRORS.md

```markdown
### Note: <short statement of the trap, not the symptom>

What did not work: <the approach and the actual observed failure>

What worked instead: <the fix, specific enough to repeat>

Note for next time: <the general lesson, one sentence>
```

## How to Use It

### In Claude Code

Install the plugin through the marketplace:

```shell
/plugin install project-context@pinkpixel-skills
```

Invoke the skill directly in your session:

```shell
/project-context
/project-context:project-context
```

You can also ask Claude Code to handle specific context tasks:

```text
/project-context "bootstrap /DOCS for this new project"
/project-context "check MEMORY.md before we refactor authentication"
/project-context "log our decision to switch from Redis to SQLite"
```

### In Other Agent Environments

If you use Codex, Antigravity, Cursor, or OpenCode, copy the skill to your agent configuration directory:

```bash
mkdir -p ~/.agents/skills
cp -r skills/project-context ~/.agents/skills/
```

Then invoke it naturally:

```text
Use the project-context skill to inspect /DOCS/MEMORY.md and verify whether we previously rejected this caching strategy.
```

## Bootstrapping a New Project

To add durable context files to a fresh repository:

1. Create a `/DOCS` directory at the project root.
2. Copy `templates/OVERVIEW.md`, `templates/MEMORY.md`, and `templates/ERRORS.md` into `/DOCS`.
3. Fill out `OVERVIEW.md` using only what the code currently demonstrates (stack, directory structure, data models, key commands).
4. Leave `MEMORY.md` and `ERRORS.md` empty apart from their headers. They fill up naturally from real tasks and real lessons.

## Examples and Reference Guides

For in-depth explanations and side-by-side good versus bad entries, consult the bundled reference documents:

- [references/overview.md](references/overview.md): Rules for keeping `OVERVIEW.md` accurate and focused.
- [references/memory.md](references/memory.md): How to write durable decision logs with real rejected alternatives.
- [references/errors.md](references/errors.md): How to record troubleshooting traps that save hours later.
- [references/examples.md](references/examples.md): Side-by-side comparisons of useful records versus unhelpful noise.

To see full, populated sample files from a real project, inspect the repository examples in [examples/project-context/](../../examples/project-context/).