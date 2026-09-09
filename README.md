# Pink Pixel Skills

A collection of agent skills and Claude Code plugins built for practical AI-assisted software development and technical writing.

This repository functions both as a standalone skill library for agent runtimes and as a Claude Code plugin marketplace.

## Available Skills

| Skill | Description | Docs |
|---|---|---|
| **[Clear Writing](skills/clear-writing/README.md)** | Write and edit technical documentation and human prose. Combines ASD-STE100 Simplified Technical English for instructional steps with an anti-AI pattern audit for voiced writing. | [Read guide](skills/clear-writing/README.md) |
| **[Handoff](skills/handoff/README.md)** | Compact the active conversation into a structured handoff document saved to your OS temporary directory so a fresh agent can continue where you stopped. | [Read guide](skills/handoff/README.md) |
| **[Pickup](skills/pickup/README.md)** | Find and load the latest relevant handoff document created by `handoff`, allowing a new session to resume immediately without re-explaining context. | [Read guide](skills/pickup/README.md) |

## Using with Claude Code

This repository is configured as a Claude Code plugin marketplace (`pinkpixel-skills`). You can register the marketplace and install plugins either interactively or through the terminal CLI.

### 1. Add the Marketplace

To register the marketplace from GitHub, run:

```shell
# Inside Claude Code
/plugin marketplace add pinkpixel-dev/skills

# Or from your terminal
claude plugin marketplace add pinkpixel-dev/skills
```

If you are testing from a local clone of this repository, pass the local path instead:

```shell
# Inside Claude Code
/plugin marketplace add ./pinkpixel-skills

# Or from your terminal
claude plugin marketplace add ./pinkpixel-skills
```

### 2. Install Plugins

Install individual plugins by specifying the plugin name and marketplace identifier (`<plugin>@pinkpixel-skills`):

```shell
# Inside Claude Code
/plugin install handoff@pinkpixel-skills
/plugin install pickup@pinkpixel-skills
/plugin install clear-writing@pinkpixel-skills

# Or from your terminal
claude plugin install handoff@pinkpixel-skills
claude plugin install pickup@pinkpixel-skills
claude plugin install clear-writing@pinkpixel-skills
```

If Claude Code prompts you to reload plugins to activate them, run:

```shell
/reload-plugins
```

### 3. Run the Skills

Once installed, invoke any skill in your session. Plugin skills are namespaced with their plugin name:

```shell
# Run handoff at the end of a session
/handoff
/handoff:handoff

# Run pickup in your next session to resume
/pickup
/pickup:pickup

# Run clear-writing to audit or rewrite documentation
/clear-writing
/clear-writing:clear-writing
```

### 4. Update Plugins and Marketplace

To fetch the latest plugin versions and marketplace updates:

```shell
# Refresh the marketplace catalog
claude plugin marketplace update pinkpixel-skills

# Update a specific plugin
claude plugin update handoff@pinkpixel-skills
```

Inside an interactive session, you can also run `/plugin marketplace update` or check the `/plugin` interface.

## Using with Other Agent Environments

If you use other coding agents or runtimes, install skills by copying the skill folder into your agent's configuration root:

- **Claude Code (manual directory):** `~/.claude/skills/<skill-name>`
- **Global Agents:** `~/.agents/skills/<skill-name>`
- **Codex:** `~/.codex/skills/<skill-name>`
- **Antigravity:** `~/.gemini/config/skills/<skill-name>`

For example, to install `handoff` into your global agents folder:

```bash
mkdir -p ~/.agents/skills
cp -r skills/handoff ~/.agents/skills/
```

## Repository Structure

```text
.claude-plugin/
  marketplace.json       Marketplace catalog manifest
skills/
  clear-writing/         Clear Writing skill documentation and configuration
  handoff/               Handoff skill instructions and plugin manifest
  pickup/                Pickup skill instructions and plugin manifest
examples/                Sample outputs and before-and-after comparisons
```

## License

This project is licensed under the Apache 2.0 License. See [LICENSE](LICENSE) for details.
