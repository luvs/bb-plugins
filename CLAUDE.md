# bb-plugins

Personal BB plugins (getbb.app), built for my own bb. The repo is public
because it costs nothing to be; it is not a product.

## Layout

One self-contained directory per plugin at the repo root, plainly named
(`todo`, not `bb-plugin-todo`), with its own `package.json`,
`package-lock.json` and `tsconfig.json`. There is no root `package.json`, no
workspaces, and no code shared between plugins.

**Why:** a plugin that outgrows this repo leaves as `git mv <dir>` into a repo
of its own, with nothing to untangle. Keep every plugin buildable from its own
directory alone.

`bb plugin new <name>` scaffolds `./bb-plugin-<name>`. Rename the directory to
`<name>`; the `bb-plugin-` prefix stays on the package `name`.

## Writing a plugin

Invoke the `bb-plugin-authoring` skill. It ships with bb and is authoritative
for the SDK — the installed bb version decides the exact API, so prefer it over
anything remembered.

Pin `@get-bb/plugin-sdk` to an exact version and keep `engines.bb` and
`engines.bbPluginSdk` honest. `bb plugin types` repins both to the running bb.

## Verifying

Run the plugin in bb before calling the work done. In the plugin directory:
`npm ci && bb plugin install .`, then `bb plugin dev` to rebuild and reload on
every change. `bb plugin logs <id>` prints its log.

Releasing to the BB store is out of scope here: plugins install locally from
their directory. A plugin worth sharing moves to its own repo first.

## Agent skills

### Issue tracker

Issues are tracked in GitHub Issues for `luvs/bb-plugins`, using the `gh` CLI.
See `docs/agents/issue-tracker.md`.

### Domain docs

Single-context: one `GLOSSARY.md` and `docs/adr/` at the repo root. See
`docs/agents/domain.md`.
