# Volver Claude Code marketplace

Agent skills for the [Volver](https://github.com/volverjs) libraries, one Claude Code plugin per
package, and the skill that scaffolds a new project from the monorepo starter. Each plugin reads
its skill from the package's own repository (`skills/` on `main`), so the skill ships with the
library and this repository only lists them.

| Plugin | Package |
|---|---|
| `volverjs-style` | `@volverjs/style` |
| `volverjs-ui-vue` | `@volverjs/ui-vue` |
| `volverjs-data` | `@volverjs/data` |
| `volverjs-query-vue` | `@volverjs/query-vue` |
| `volverjs-form-vue` | `@volverjs/form-vue` |
| `volverjs-zod-vue-i18n` | `@volverjs/zod-vue-i18n` |
| `volverjs-auth-vue` | `@volverjs/auth-vue` |
| `volverjs-monorepo-starter` | `@volverjs/monorepo-starter`, the project template |

## Install

```bash
/plugin marketplace add volverjs/claude-plugins
/plugin install volverjs-style@volverjs
```

Install the plugins of the packages a project uses. To offer them to everyone who works on a
project, declare the marketplace and the plugins in the project's `.claude/settings.json`
(`extraKnownMarketplaces` and `enabledPlugins`): each member confirms the install once.
`volverjs-monorepo-starter` belongs to no project: install it once, for your user, and ask
Claude Code for a new project wherever you want it created.

Claude Code clones `github` sources over SSH. Without an SSH key for GitHub the install fails
with `Permission denied (publickey)`; either add a key or rewrite the URL:
`git config --global url."https://github.com/".insteadOf git@github.com:`.

Agents other than Claude Code install the same skills with the
[skills CLI](https://github.com/vercel-labs/skills): `npx skills add volverjs/style`.

## Adding a package

1. The package keeps its skill in `skills/<skill-name>/SKILL.md` on `main`. A skill on a
   development branch would describe an API that is not released yet.
2. Add an entry to `.claude-plugin/marketplace.json` with a `github` source pinned to
   `"ref": "main"`, `strict: false` and `skills: ["./skills/"]`. Without the `ref` the source
   reads the default branch, which is `develop` in the Volver repositories.
   A repository with its own `.claude-plugin/plugin.json`, like
   the monorepo starter, gets neither: its manifest declares the skills, and `strict: false`
   next to it fails to load with `conflicting manifests`.
3. Check it: `claude plugin validate --strict .`. The validation does not fetch `github`
   sources, so a conflicting entry only shows up once installed (`claude plugin list`).
