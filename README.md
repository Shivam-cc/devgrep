# devgrep

Content-aware source retrieval for coding agents.

Ask a question about a repository, and devgrep returns the relevant files,
declaration locations and verbatim source excerpts. A coding agent can then start
unfamiliar multi-file work with useful context. The agent still owns
implementation and verification.

```sh
npm install -g devgrep
dg auth
dg "How are telemetry events recorded and sent?" ./my-project
```

Requires Node.js 22 or newer on macOS, Linux or Windows. The package installs two
equivalent commands, `devgrep` and `dg`.

## How it works

devgrep explores the repository hierarchically. It uses directory metadata and
content previews to decide where to look, instead of uploading the whole tree.
Jev, TypeSafe's classification model, judges which content is relevant to the
question. Relevant files are printed to stdout as a summary, ranked locations and
source excerpts. Retrieved source is data, never instructions. See
[docs/architecture.md](docs/architecture.md).

## Providers

`dg auth` asks you to choose a provider, then saves its key in a local config file:

- Vercel AI Gateway (`vercel`)
- TypeSafe (`typesafe`)
- OpenRouter (`openrouter`)
- OpenCode Zen (`opencode`)
- Any TypeSafe-compatible endpoint (`custom`)

Run `dg doctor` to verify access. Keys come only from saved credentials, never from
environment variables. Searches send eligible source to the saved provider. Run
`dg files ./my-project` to see what a search may read; it needs no key and sends
nothing.

## Agent skill

Installing the CLI is only half of agent setup. Install the skill into the project
where your coding agent works:

```sh
dg skill
```

Or run the skills installer directly:

```sh
npx skills add Shivam-cc/devgrep --skill devgrep
```

## Documentation

- [CLI reference](apps/cli/README.md): auth, custom gateways, storage, caching and output
- [Architecture](docs/architecture.md)
- [Evaluations](evals/README.md)

## Development

This is a Bun 1.3.14 workspace.

```sh
bun install --frozen-lockfile
bun run verify
```

`verify` runs type checks, lint, and the test suites. The test suites run in
Docker. `bun run format:check` checks formatting.

## License

[MIT](LICENSE)
