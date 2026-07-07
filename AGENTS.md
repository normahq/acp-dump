# acp-dump Agent Notes

`acp-dump` is a small Go CLI that starts a stdio Agent Client Protocol (ACP)
server command, initializes it, creates a session, and prints the provider
metadata for inspection.

## Project Layout

- `cmd/acp-dump/main.go`: executable entrypoint.
- `cmd/acp-dump/cmd/command.go`: Cobra command, flags, examples, and argument validation.
- `internal/apps/acpdump`: ACP inspection workflow and output formatting.
- `internal/apps/appio`: synchronized writer helpers.
- `internal/logging`: process-wide structured logging setup.

## Development Rules

- Keep stdout reserved for user-facing inspection output. Debug and provider
  process logs must go to stderr.
- Keep ACP provider examples in README/help current with supported providers.
  Do not add abandoned provider examples.
- Preserve the `-- <acp-server-cmd> [args...]` contract. Arguments before `--`
  are CLI flags; arguments after it are passed to the ACP server.
- Prefer small, focused changes. Avoid unrelated workflow, orchestration, or
  product-policy docs in this repository.

## Commands

```sh
task test
task lint
task
```

Equivalent direct commands:

```sh
go test ./...
go tool golangci-lint run ./...
go build -o bin/acp-dump ./cmd/acp-dump
```
