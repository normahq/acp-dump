# acp-dump

[![test](https://github.com/normahq/acp-dump/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/normahq/acp-dump/actions/workflows/test.yml)
[![lint](https://github.com/normahq/acp-dump/actions/workflows/lint.yml/badge.svg?branch=main)](https://github.com/normahq/acp-dump/actions/workflows/lint.yml)
[![security](https://github.com/normahq/acp-dump/actions/workflows/security.yml/badge.svg?branch=main)](https://github.com/normahq/acp-dump/actions/workflows/security.yml)
[![release](https://github.com/normahq/acp-dump/actions/workflows/omnidist-release.yml/badge.svg)](https://github.com/normahq/acp-dump/actions/workflows/omnidist-release.yml)
[![npm](https://img.shields.io/npm/v/@normahq/acp-dump)](https://www.npmjs.com/package/@normahq/acp-dump)
[![License](https://img.shields.io/github/license/normahq/acp-dump)](LICENSE)
[![Version](https://img.shields.io/github/v/tag/normahq/acp-dump?label=version)](https://github.com/normahq/acp-dump/tags)

**Inspect ACP agents before wiring them into your workflow.**

`acp-dump` starts any stdio Agent Client Protocol (ACP) server command and
prints the initialize/session data you need to trust, debug, or compare it.

Use it when an ACP provider says it supports models, modes, auth, sessions, or
capabilities, and you want to see exactly what it reports before building
against it.

## What You Get

| Capability | Behavior |
| --- | --- |
| ACP preflight | Starts a stdio ACP server command and initializes a session. |
| Capability inventory | Prints protocol version, agent capabilities, auth methods, and session details. |
| Model and mode discovery | Shows available session models and modes when the provider exposes them. |
| JSON output | Emits machine-readable output for scripts, CI checks, and debugging artifacts. |
| Quiet by default | Keeps inspector lifecycle logs out of the result unless `--debug` is enabled. |
| Provider agnostic | Works with OpenCode, Codex, Claude Code, Pi, and any executable that speaks ACP over stdio. |

## Try It

Install globally:

```sh
npm install -g @normahq/acp-dump@latest
```

Run once with `npx`:

```sh
npx @normahq/acp-dump@latest -- <acp-server-cmd> [args...]
```

Inspect an ACP server:

```sh
acp-dump -- opencode acp
acp-dump --json -- opencode acp
acp-dump -- npx -y @normahq/codex-acp-bridge@latest
acp-dump -- npx -y @zed-industries/claude-code-acp@latest
acp-dump --debug -- npx -y pi-acp
```

## Provider Commands

| Provider | Command |
| --- | --- |
| OpenCode | `acp-dump -- opencode acp` |
| Codex | `acp-dump -- npx -y @normahq/codex-acp-bridge@latest` |
| Claude Code | `acp-dump -- npx -y @zed-industries/claude-code-acp@latest` |
| Pi | `acp-dump -- npx -y pi-acp` |
| Generic ACP | `acp-dump -- <acp-server-cmd> [args...]` |

The `--` separator is required. Arguments before `--` are treated as
`acp-dump` flags; arguments after it are passed to the ACP server command.

## Output

Human-readable output includes:

- agent name and version
- protocol version
- ACP capabilities
- auth methods
- session id
- available session modes and models when provided by the server

Use `--json` when you want stable output for scripts, test fixtures, issue
reports, or CI logs.

## Use Cases

- Verify a provider's ACP surface before connecting it to an agent runtime.
- Compare model, mode, auth, and capability metadata across ACP providers.
- Capture a compact diagnostic artifact for bug reports.
- Check whether a local command is actually speaking ACP over stdio.

## Flags

| Flag | Purpose |
| --- | --- |
| `--json` | Print machine-readable JSON output. |
| `--debug` | Enable debug logs for the inspector. |
| `-h`, `--help` | Show command help. |

## Repository

- GitHub: <https://github.com/normahq/acp-dump>

## Contact

- Issues: <https://github.com/normahq/acp-dump/issues>
- Maintainer: [@metalagman](https://github.com/metalagman)

## License

MIT. See the repository [LICENSE](https://github.com/normahq/acp-dump/blob/main/LICENSE).
