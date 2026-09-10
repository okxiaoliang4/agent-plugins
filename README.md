# Jelf Agent Skills

This repository is a private Agent Plugins package containing the reusable skills from `~/.agents/skills`.

## Layout

- `plugin.json` — Agent Plugins v1 manifest.
- `skills/<skill-name>/SKILL.md` — discoverable Agent Skills and their bundled references, scripts, and assets.

There is no `mcp.json` because this package currently provides skills only.

## Source snapshot

The initial snapshot was imported from `/Users/jelf/.agents/skills`. Home Manager/Nix symlinks were materialized as regular files so the package is self-contained and satisfies the Agent Plugins path-containment rules. Local `.git` history, `.DS_Store`, and `*.hm-backup-*` backup artifacts were intentionally left out.

The source directory is managed by other tooling, so update this repository by reviewing and importing a fresh snapshot rather than replacing the source directory with a checkout.

## Specification

The package targets Agent Plugins Specification 1.0.0:

<https://agent-plugins.org/specification>
