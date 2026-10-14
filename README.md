# Genero Claude skills

Shared Claude skills for the Genero team. Public, so anyone can install it without logging in, whichever claude.ai organization they are in.

## Install

### Claude Code

Run once:

```
/plugin marketplace add generoi/claude-skills
/plugin install genero-design@genero
```

Get updates with `/plugin marketplace update genero`.

### claude.ai (web, desktop app)

1. Open the [latest release](../../releases/tag/latest) and download the skill's zip, for example `genero-kickoff-to-design.zip`.
2. In claude.ai, go to Settings, then Skills, and upload the zip.

Repeat when a skill changes. The release is rebuilt on every change to `main`.

## Skills

| Plugin | Skill | What it does |
|---|---|---|
| genero-design | `genero-kickoff-to-design` | Builds a Claude Design canvas for a new project: a Kickoff / Workshop page (brief, users, journeys, sitemap, page-type wireframes, open questions) and, after the workshop, a Design page on GDS tokens with every sitemap page. |

## Add or change a skill

1. Create a branch.
2. Add a folder under `plugins/<plugin>/skills/<skill-name>/` with a `SKILL.md` (front matter: `name`, `description`).
3. Open a PR. Someone from the core team reviews it.
4. When the plugin's behaviour changes, bump `version` in `plugins/<plugin>/.claude-plugin/plugin.json`.

Keep skills based on GDS (generoi/bedrock). This repo is public: never put client data, credentials or personal details in a skill.
