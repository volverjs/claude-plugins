# Volver Claude Code marketplace

Agent skills for the [Volver](https://github.com/volverjs) libraries, one Claude Code plugin per
package. Each plugin reads its skill from the package's own repository (`skills/` on `main`),
so the skill ships with the library and this repository only lists them.

| Plugin | Package |
|---|---|
| `volverjs-style` | `@volverjs/style` |
| `volverjs-ui-vue` | `@volverjs/ui-vue` |
| `volverjs-data` | `@volverjs/data` |
| `volverjs-query-vue` | `@volverjs/query-vue` |
| `volverjs-form-vue` | `@volverjs/form-vue` |
| `volverjs-zod-vue-i18n` | `@volverjs/zod-vue-i18n` |
| `volverjs-auth-vue` | `@volverjs/auth-vue` |

## Install

```bash
/plugin marketplace add volverjs/claude-plugins
/plugin install volverjs-style@volverjs
```

Install the plugins of the packages a project uses. To offer them to everyone who works on a
project, declare the marketplace and the plugins in the project's `.claude/settings.json`
(`extraKnownMarketplaces` and `enabledPlugins`): each member confirms the install once.

Claude Code clones `github` sources over SSH. Without an SSH key for GitHub the install fails
with `Permission denied (publickey)`; either add a key or rewrite the URL:
`git config --global url."https://github.com/".insteadOf git@github.com:`.

Agents other than Claude Code install the same skills with the
[skills CLI](https://github.com/vercel-labs/skills): `npx skills add volverjs/style`.

## Adding a package

1. The package keeps its skill in `skills/<skill-name>/SKILL.md` on `main`. A skill on a
   development branch would describe an API that is not released yet.
2. Add an entry to `.claude-plugin/marketplace.json` with a `github` source, `strict: false`
   and `skills: ["./skills/"]`.
3. Check it: `claude plugin validate --strict .`
