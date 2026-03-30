# Mila Skill for OpenClaw

An [OpenClaw](https://clawhub.ai) skill that teaches AI agents how to use the [Mila](https://mila.gg) REST API and MCP tools to manage documents, spreadsheets, and slide presentations.

## What is OpenClaw?

[OpenClaw](https://clawhub.ai) is a package manager for AI agent skills. Skills are structured reference files that give agents domain knowledge — like API docs, best practices, and usage patterns — so they can perform tasks without needing everything hardcoded into their system prompt.

When a user installs a skill, the agent downloads the skill files into its local workspace (typically `~/.openclaw/workspace/skills/<name>/`) and loads them as context when relevant tasks come up.

## How it works

This repo contains a `SKILL.md` file (the skill manifest) and a `references/` directory with detailed API documentation:

```
mila-skill/
  SKILL.md                    # Manifest: metadata, auth, MCP setup, quick start, tool list
  references/
    DOCUMENTS.md              # 6 endpoints for document CRUD + append
    SHEETS.md                 # 10 endpoints for workbook/tab/cell operations
    SLIDES.md                 # 6 endpoints for presentation CRUD + append
    SERVERS.md                # 1 endpoint for listing workspaces
```

When an agent has this skill installed, it knows how to:
- Authenticate with Mila API keys (`mila_sk_*`)
- Create, read, update, and delete documents with HTML content
- Manage spreadsheets with A1 cell notation, formulas, and cell formatting
- Build slide presentations with free-form HTML on a 960x540 canvas
- Connect to the MCP server for tool-based interaction
- Filter content by server (workspace) and paginate results

## Install

Ask any OpenClaw-compatible agent:

```
Can you install this skill please? https://clawhub.ai/freddyjd/mila
```

The agent downloads and installs it automatically. Then give it your API key:

```
Here is the API key: mila_sk_your_key_here
```

Create an API key at [mila.gg/api-keys](https://mila.gg/api-keys) (individual) or [mila.gg/team-api](https://mila.gg/team-api) (teams).

## Publishing

This repo auto-publishes to [ClawHub](https://clawhub.ai) via GitHub Actions whenever `SKILL.md` or anything in `references/` changes on `main`.

The workflow (`.github/workflows/publish-clawhub.yml`):
1. Extracts the `version` from `SKILL.md` frontmatter
2. Checks if that version already exists on ClawHub
3. If not, publishes using `bunx clawhub@latest publish`

To release a new version: bump the `version` field in `SKILL.md` and push to `main`.

## Links

- [Skill on ClawHub](https://clawhub.ai/freddyjd/mila)
- [Mila](https://mila.gg)
- [Mila Documentation](https://mila.gg/spec)
- [MCP Server](https://github.com/mila-gg/mcp-server)
