# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is

This is a **documentation-only** repository containing a ChatGPT Custom Skill (`contakt-project-setup`). There is **no application code, no build system, no package manager, and no runtime services**. The product is a zip file of Markdown + YAML files that gets uploaded to ChatGPT's Skills feature.

### Key files

- `SKILL.md` — main workflow definition (source of truth)
- `references/` — templates referenced by SKILL.md
- `agents/openai.yaml` — ChatGPT surface config
- `contakt-project-skill.zip` — pre-built skill package for upload
- `README.md` — installation instructions (in Dutch)

### Linting

You can lint markdown files with `pymarkdown`:

```
pymarkdown scan SKILL.md README.md references/folder-structure.md references/project-context-template.md
```

Existing files have style warnings (line-length, spacing) but no structural errors. The project has no `.markdownlint` config, so default rules apply.

### Testing / validation

There are no automated tests. Validate changes by:

1. Checking markdown syntax with `pymarkdown scan <file>`
2. Validating `agents/openai.yaml` parses as valid YAML
3. Verifying the zip file (`unzip -t contakt-project-skill.zip`) contains `SKILL.md`, `references/`, and `README.md`
4. If `SKILL.md` or references change, the zip must be rebuilt: `zip -r contakt-project-skill.zip SKILL.md references/ agents/ README.md`

### No services to run

There are no dev servers, databases, or background processes. The "deployment" is uploading the zip to ChatGPT via Settings > Skills.

### Language

All content is written in Dutch. Keep documentation and skill content in Dutch unless the user requests otherwise.
