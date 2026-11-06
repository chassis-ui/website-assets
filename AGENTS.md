# AGENTS.md

Instructions for AI coding agents working in this repository. It holds the rules an agent
breaks without being told; the README explains the rest.

## Project

@chassis-ui/website-assets holds design files: fonts, images, icons and others, by brand and app. They are built
with [`@chassis-ui/assets`](https://www.npmjs.com/package/@chassis-ui/assets) from
`source/<brand>/<app>/<type>/` to `dist/<platform>/<app>/<brand>/`. The build is file-driven: a
file added to `source/` is in the output, with no list to update.

## Commands

Once, with Node.js 22.12 or later and Git LFS installed: `git lfs install`, then `pnpm install`.

| Command                   | What it does                                                 |
| ------------------------- | ------------------------------------------------------------ |
| `pnpm lint`            | Checks the names and the layout of `source/`                 |
| `pnpm build`           | Builds into `dist/`                                          |
| `pnpm build:release`   | The build of a release                                       |
| `pnpm verify`          | Checks `dist/` against `source/` and `chassis.checks.json`   |
| `pnpm release-notes`   | Prints the changelog entry of the version, or fails          |

## Rules

- **Edit `source/`, never `dist/`.** `dist/` is the output of a build and is not committed.
- **Keep the layout.** `_default` holds the files of every brand, `_shared` beside the apps of a
  brand the files of every app. A brand file replaces the default file of the same path, and
  an app file the shared file. A name that starts with `_` is no brand and no app.
- **The names in `dist/` are public.** Consumers read them by name. Renaming or removing a file
  of `source/` breaks them, so the changelog says so, and `chassis.checks.json` lists the files
  that are checked after a build.
- **Do not get past the source lint.** Fix the file; do not add an entry to `lint.allow` of
  `chassis.checks.json` unless the maintainer asks for it.
- **Do not remove an asset** because nothing reads it today. That is the maintainer's decision.
- **Fonts and raster images are Git LFS files.** Do not commit one as a plain file, and do not
  read a pointer file as if it were the font or the image.

## Branches

- `main` holds the released versions, and takes a change by pull request only.
- `next` is the prerelease channel. Work is merged into it first, and it is merged into `main`
  with a merge commit, never a squash, so the two keep one history.
- Any other branch is short-lived, `feat/…`, `fix/…` or `chore/…`, and is squash-merged.

## Releases

A push to `main` or `next` with a new version in `package.json` releases it, so:

- On `next`, only a version with a prerelease part, such as `0.4.0-next.0`, is released, as a
  prerelease; on `main`, any new version. Each version, a prerelease too, has its entry.
- A new version and its entry in `CHANGELOG.md` go in one commit. The release stops without the
  entry. The entry names the files of `dist/` that are added, removed or renamed.
- Before that commit, run `pnpm lint`, `pnpm build:release` and `pnpm verify`.
- Do not push, tag or raise the version unless asked.
