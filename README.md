# Innocitto Bricks Agents

Agent documentation for Innocitto Bricks Builder web projects. Harness-agnostic instructions that any AI coding tool can follow via `AGENTS.md`.

## Stack (Bricks edition)

This version is adapted for WordPress sites built with:

- **[Bricks Builder](https://bricksbuilder.io/) 2.2+**: page builder and theme
- **Bricks Native Framework (Bricksmaven)**: design tokens defined in the Bricks Style Manager (variables, the "BM - Colors" palette, the global theme style). No third-party CSS framework. Root font size is 10px (1rem = 10px).

## Install into a project

From any project directory:

```bash
npx innocitto-bricks-agents
```

Or specify a target directory:

```bash
npx innocitto-bricks-agents ./my-wordpress-site
```

This copies `AGENTS.md` and `agent-docs/` into the target and scaffolds `discovery/brief.md` (an empty discovery brief stub). Your AI coding tool reads `AGENTS.md` and loads the referenced docs — no harness-specific skill folders required.

Use `--force` to overwrite existing files:

```bash
npx innocitto-bricks-agents --force
```

## Start a project

After installing, open the project in your AI coding tool and say:

```
start discovery
```

The agent runs a guided 7-phase discovery interview (project goal, business, audience, competitors, pages, brand, proof) focused purely on marketing, copy, and design inputs, grilling you for specifics and pushing back on vague answers. It fills in `discovery/brief.md` as it goes — the file is created at install time so discovery progress is always checkable — and that brief becomes the source of truth for copywriting, wireframing, and design. See [agent-docs/discovery.md](agent-docs/discovery.md) for the full playbook.

## Structure

```
├── AGENTS.md       # Entry point — workflow, stack, doc index
├── templates/      # Files scaffolded into projects
│   └── discovery-brief.md   # Stub copied to discovery/brief.md on install
└── agent-docs/     # Reference docs loaded by workflow step
    ├── discovery.md    # Guided discovery interview (step 1)
    ├── copywriting.md
    ├── design.md
    ├── bricks.md       # Bricks structure, classes, templates, JSON delivery
    ├── bnf.md          # Bricks Native Framework index + global rules
    ├── bnf/            # Token references (colors, typography, spacing, layout, …)
    ├── css.md
    └── html.md
```

## Development

Test the CLI locally before publishing:

```bash
node bin/cli.js /tmp/test-project
```

### Releasing

Publishing to npm is automated. A GitHub Actions workflow (`.github/workflows/publish.yml`) runs on every push to `main` and publishes only when the version in `package.json` is new. To cut a release:

```bash
npm version patch   # bumps version + creates a git tag (use minor/major as needed)
git push --follow-tags
```

The workflow checks npm, sees the new version, and publishes it. Pushes without a version bump are ignored (no error).

**Authentication:** the workflow uses npm [Trusted Publishing](https://docs.npmjs.com/trusted-publishers), so no npm token is stored in GitHub. It's configured on npmjs.com under the package's **Settings → Trusted Publisher** (GitHub Actions, user `citto-cyber`, repository `Citto-Agents`, workflow `publish.yml`). Each release also gets a provenance badge on npm automatically.

To publish manually instead:

```bash
npm publish
```

## Usage (manual)

You can also copy or symlink `AGENTS.md` and `agent-docs/` into a client project by hand.

## Credits

Adapted from [gearyco-agentic-web-design](https://github.com/kevingeary/gearyco-agentic-web-design) by Kevin Geary (MIT license), retargeted from Etch + Automatic.css to Bricks Builder + the Bricksmaven Bricks Native Framework.
