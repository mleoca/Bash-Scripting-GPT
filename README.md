# Shell Expert Pro

A manual that teaches AI agents to write production-quality bash scripts.

## Usage

Copy [prompt.md](prompt.md) into your AI's system prompt or context.

### As a Claude Code Skill

```bash
mkdir -p .claude/skills/bash-expert
curl -sL https://raw.githubusercontent.com/mleoca/Bash-Scripting-GPT/main/SKILL.md -o .claude/skills/bash-expert/SKILL.md
curl -sL https://raw.githubusercontent.com/mleoca/Bash-Scripting-GPT/main/prompt.md -o .claude/skills/bash-expert/prompt.md
```

### As an OpenAI Codex Skill

```bash
mkdir -p .codex/skills/bash-expert
curl -sL https://raw.githubusercontent.com/mleoca/Bash-Scripting-GPT/main/SKILL.md -o .codex/skills/bash-expert/SKILL.md
curl -sL https://raw.githubusercontent.com/mleoca/Bash-Scripting-GPT/main/prompt.md -o .codex/skills/bash-expert/prompt.md
```

## License

MIT
