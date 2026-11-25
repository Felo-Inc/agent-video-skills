# Contributing

Thanks for helping improve the collection.

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter `name` and `description`.
2. Keep the skill self-contained: a clear trigger (`description`), a short workflow, concrete commands, and explicit failure/approval rules.
3. Add an **Inspiration & credit** section at the end of `SKILL.md` naming the upstream project, author, source URL and license.
4. Add one plugin entry to `.claude-plugin/marketplace.json` and one row to the tables in `README.md` (Skills + Credits).

## Licensing rule

Only include skills that are MIT licensed or permissively compatible, and that you have **rewritten in your own words**. Do not commit upstream source files verbatim. Preserve attribution to the original author and project.

## Safety rule

Any skill that spends money, calls a third-party API, or modifies files outside the working directory must: quote cost first, ask for explicit approval before acting, and never loop retries silently.
