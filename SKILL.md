---
name: bash-expert
description: Direct delivery of production-quality bash scripts with optional Logic Map planning
version: 5.0.0
author: Mihail Constantin Leoca
triggers:
  - bash script
  - shell script
  - write a script
  - automation script
  - sys admin script
---

# Bash Expert Skill

Generate production-quality bash scripts with direct delivery. No skeletons. No staging. Just working code.

## What This Skill Does

**DEFAULT:** Delivers complete, working scripts directly.

**ON REQUEST:** Shows Logic Map (scannable planning format) when you ask for "plan", "design", or "structure".

Scripts always include:

- **Strict mode**: `set -euo pipefail` in every script
- **Quoted variables**: `"${var}"` to prevent word splitting
- **Error handling**: `if ! command; then` pattern
- **Modular design**: `main()` function, single-responsibility functions
- **Signal handling**: `trap` for cleanup on EXIT, INT, TERM
- **ShellCheck compliant**: Zero errors, zero warnings

## Invocation

### Explicit
```
/bash-expert Check if a file exists and print its size
```

### Automatic Detection
The skill auto-triggers when you ask for:
- Bash or shell scripts
- System automation
- DevOps tooling
- File processing scripts
- Backup/deployment scripts

## Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `--style` | `linear` (simple) or `modular` (complex) | auto-detect |
| `--bash-version` | Target version (3.2, 4.x, 5.x) | 4.0+ |
| `--plan` | Show Logic Map before implementation | false |

## Output Modes

### Direct Delivery (Default)
Complete working script with no explanatory prose.

### Logic Map (On Request)
When you say "plan", "design", or use `--plan`:

```
## Logic Map: backup-system

### Data Flow
INPUT → config → PROCESS → compress → OUTPUT → remote

### Functions (Complexity)
├── parse_config()      #simple  → returns: config_array
├── compress_files()    #complex → returns: archive_path
└── main()             #simple  → orchestrates all

### Error Strategy
- Config missing: EXIT with usage
- Compression fail: LOG + return 1

### Dependencies
- External: tar, gpg
```

Then asks: "Proceed with implementation?"

## Examples

### Simple Script
```
/bash-expert Check disk usage and alert if over 80%
```

### With Planning
```
/bash-expert --plan Create a backup system with compression and remote sync
```

### macOS Compatible
```
/bash-expert --bash-version 3.2 Parse CSV without associative arrays
```

## Key Patterns

### Error Handling
```bash
if ! command; then
    printf "Error: command failed\n" >&2
    return 1
fi
```

### Variable Declaration
```bash
local var
var=$(command) || return 1
if [[ -z "${var}" ]]; then
    printf "Error: empty result\n" >&2
    return 1
fi
```

### Cleanup Pattern
```bash
cleanup() {
    local ec=$?
    rm -rf "${TEMP_DIR:-}"
    exit "$ec"
}
trap cleanup EXIT INT TERM
```

## Related Files

- `prompt.txt` - Full system prompt (~550 lines)

## Testing

Validated against test cases across categories:
- Error Handling, Variables, Functions, Structure
- Input Validation, File Ops, Compatibility, Security

Scripts tested across Bash 3.2, 4.4, 5.0, 5.1, and 5.2.
