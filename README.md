# EGA Atlas Site

Read-only Quartz 5 site for [EGA Atlas](https://github.com/egawilldoit/ega-atlas).
All published knowledge is pulled from `ega-atlas@main` during GitHub Actions builds;
this repository contains the website and does not own any Atlas knowledge.

## Live site

Once Pages is enabled (Settings → Pages → Source: GitHub Actions), open
https://egawilldoit.github.io/ega-atlas-site/

## Build / content synchronization

The [deployment workflow](.github/workflows/deploy.yml) deploys on `v5`
pushes, manual dispatch and an hourly safety-net schedule. It also supports
`repository_dispatch` with type `atlas-updated` if an immediate trigger is
configured later. Scheduled runs are not guaranteed to execute on time.

In an ephemeral local clone (requires Node.js 22+, npm 10.9.2+):

```sh
npm ci
npx quartz plugin install --from-config
rm -rf content
git clone --depth 1 https://github.com/egawilldoit/ega-atlas.git content
npx quartz build --serve
```

The public site is a subset: `index.md`, `now.md`, `log.md`, and `wiki/`.
It excludes `raw/`, `templates/`, `.agents/`, `AGENTS.md`, and other tooling.
Never assume site exclusions make files private in the public source repository.

Keep links relative in Markdown. Editors and agents must continue writing only
in the original EGA Atlas repository, following its `AGENTS.md`.

**Never edit content in this repository.** Do not build a new database,
authentication, or editorial interface for this read-only site.
