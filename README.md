# Shell Expert Pro

Production-quality bash script generation for **Claude Code** and **OpenAI GPT**.

[![Version](https://img.shields.io/badge/version-5.0.0-blue.svg)](https://github.com/mleoca/shell-expert-pro/releases)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

## Features

Every script generated includes:

- **Strict Mode**: `set -euo pipefail` in every script
- **Variable Quoting**: `"${var}"` everywhere to prevent word splitting
- **Error Handling**: `if ! command; then` pattern for graceful failures
- **Modular Design**: `main()` function with single-responsibility functions
- **Signal Handling**: `trap` for cleanup on EXIT, INT, TERM
- **ShellCheck Compliant**: Zero errors, zero warnings

## Usage

### OpenAI GPT

Visit [Shell Expert Pro GPT](https://chat.openai.com/g/g-jaiZcNIme-shell-expert-pro)

### Claude Code

Copy [SKILL.md](SKILL.md) and [prompt.md](prompt.md) to your `.claude/skills/bash-expert/` directory.

## v5 Prompt

The v5 prompt is a 546-line comprehensive bash scripting manual organized into 5 chapters:

1. **Chapter I: Responsibility and Ownership** - YOU own every line of code
2. **Chapter II: Problem Solving** - ANALYZE before coding
3. **Chapter III: Script Planning** - LINEAR vs MODULAR, Logic Map format
4. **Chapter IV: Bash Scripting Guidelines** - Error handling, variables, efficiency
5. **Chapter V: Output Format** - Direct delivery, CODE ONLY

[View the full prompt](prompt.md)

## Example Output

```bash
#!/bin/bash
set -euo pipefail

# Disk usage monitoring script

THRESHOLD=80

check_disk_usage() {
    local mount_point="$1"
    local usage

    if ! usage=$(df "${mount_point}" | awk 'NR==2 {print $5}' | tr -d '%'); then
        printf "error: failed to get disk usage for %s\n" "${mount_point}" >&2
        return 1
    fi

    if [[ "${usage}" -gt "${THRESHOLD}" ]]; then
        printf "ALERT: %s is at %d%% (threshold: %d%%)\n" "${mount_point}" "${usage}" "${THRESHOLD}"
        return 1
    fi

    printf "OK: %s is at %d%%\n" "${mount_point}" "${usage}"
}

main() {
    local mount_point="${1:-/}"

    if ! check_disk_usage "${mount_point}"; then
        return 1
    fi
}

main "$@"
```

## Files

| File | Description |
|------|-------------|
| [prompt.md](prompt.md) | The complete v5 bash scripting manual (546 lines) |
| [SKILL.md](SKILL.md) | Claude Code skill definition and usage examples |

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

**Mihail Constantin Leoca** - [@mleoca](https://github.com/mleoca)

## Changelog

### v5.0.0 (2025-12-26)

- Complete rewrite with direct delivery philosophy
- Removed skeleton/staging ceremony
- Added Logic Map format for optional planning
- 48% size reduction (1045 → 546 lines)
- Dual-platform support (Claude Code + OpenAI GPT)
