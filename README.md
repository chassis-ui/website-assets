# chassis-website-assets

The assets of chassis-website-assets: fonts, images, icons and other design files, by brand and app, built
with [`@chassis-ui/assets`](https://www.npmjs.com/package/@chassis-ui/assets) into the names
and the formats of the web, iOS and Android.

## Layout

```
source/<brand>/<app>/<type>/   The files of one brand and one app: fonts/, images/, icons/, …
source/<brand>/_shared/<type>/ The files of every app of a brand
source/_default/               The files every brand gets, unless a brand has its own
dist/<platform>/<app>/<brand>/ The output of a build, not committed
package.json                   The brands, the apps and their platforms, in `chassis.build`
chassis.checks.json            The files that consumers read by name, checked after a build
```

A brand file replaces the default file of the same path, and an app file the shared file.
The build copies what is there: a designer adds a file, and the build does the rest.

## Commands

Once, with Node.js 22.12 or later and [Git LFS](https://git-lfs.com) installed:

```shell
git lfs install
pnpm install
```

| Command           | What it does                                                                |
| ----------------- | --------------------------------------------------------------------------- |
| `pnpm build`   | Builds every brand, app and platform into `dist/`                           |
| `pnpm lint`    | Checks the names and the layout of `source/`                                |
| `pnpm verify`  | Checks an existing `dist/` against `source/` and `chassis.checks.json`      |
| `pnpm archive` | Writes one zip per platform, app and brand of `dist/` to `archives/`        |
| `pnpm analyze` | Reports the sizes, the types and the duplicates of `source/` and of `dist/` |

`npx chassis-assets build --help` prints the options of the build: a part of the output with
`--brand`, `--app` and `--platform`, and the conversions that load a package.

## Releases

A release is a tag: `git tag v<version> && git push origin v<version>`, with the version of
`package.json`. The release workflow builds every job with `pnpm build:release`, verifies it,
and attaches one `<name>-<platform>-<app>-<brand>-<version>.zip` per job to the GitHub
release.

`build:release` is `chassis-assets build --optimize --subset`: the images are optimized, and
the web fonts keep the characters of the ranges of `chassis.subset` only: `latin`,
`latin-ext`, `symbols2` and the arrows `U+2190-2193`, the union of what the Chassis sites set,
and `cyrillic` and `greek` for the film titles of sinefil.org. They are split by range, so a page downloads the file of a range only when it has a character
of it. A release is what the Chassis sites and sinefil.org serve. `pnpm build` stays the
plain build, for CI and for work on the assets.

## The Chassis sites

Every Chassis documentation site vendors this repository as the Git submodule `vendor/assets`
and builds the job it reads with the two commands below, which `chassis-docs vendor` of
`@chassis-ui/docs` runs. The result, `dist/web/docs/chassis/`, is copied to `/static/` of the
site. The files a site reads by name are `contracts` of `chassis.checks.json`, and
`pnpm verify` checks them after a build.

```shell
pnpm install --ignore-workspace
pnpm assets:site
```

`assets:site` is `chassis-assets build --clean --brand chassis --app docs`, and takes the
options of the build, such as `--subset latin --split` for the fonts of a site. sinefil.org
takes the archive of its job from a release instead.

## Documentation

The [documentation of Chassis Assets](https://chassis-ui.com/assets/) describes each asset
type, the rules of each platform and how a project uses the output.

## Known oddities

Kept on purpose until the maintainer says otherwise. Do not fix one without a release note
that says what breaks.

- Eight screenshots under `images/figma/` carry a Figma export number after the resolution
  indicator, `card-orientation-top-2x-1.png`. The web build wrote that name from
  `card-orientation-top@2x-1.png`, and the sources were renamed to the output names on
  2026-09-30, so `chassis-figma` keeps reading them. They are not `@2x` files to the build.
- Eight screenshots under `images/figma/components/` are Figma export copies of another
  screenshot, `card-orientation-top-1.png` and `card-orientation-top-2x-1.png` beside
  `card-orientation-top.png`, in both modes and without `@2x`. No page of `chassis-figma`
  reads them. The contract check requires both modes for them, and not the `@2x`: they are
  the `except` patterns of the screenshot set in `chassis.checks.json`.
- `source/_default/demo/icons/icons/chassis-icons.min.css` breaks the naming rules;
  `pnpm lint` warns about it (`lint.allow` of `chassis.checks.json`).
- The copy of `@chassis-ui/icons` under `icons/icons/` and `icons/svgs/` of
  `source/_default/demo/` is the build output of `@chassis-ui/icons`, made by hand, so it is
  as new as its last refresh: 0.3.1, on 2026-10-01. Refresh it by the steps of "Refreshing
  the icons" in `docs/architecture.md` of chassis-ui/assets; do not edit it.

## Fonts

[docs/fonts.md](docs/fonts.md) lists the font files a brand holds and the steps that prepare
them, with `build/instance-font.py`, the instancer of a variable font.
