# Changelog

The notable changes of each release of `@chassis-ui/website-assets`, in the form of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Written by hand, in the commit that
sets the version. The body of the GitHub release is the entry of its version, and a version
without an entry is not released.

The history of the files before 0.1.0 is in the
[changelog of Chassis Assets](https://github.com/chassis-ui/assets/blob/main/packages/assets/CHANGELOG.md).

## [0.6.0]

The web archives of the `docs` app of both brands change, and the other archives do not. Needs
`@chassis-ui/assets` 0.12.1 to build.

### Added

- The hero illustrations of the docs sites, in `web/docs/<brand>/images/illustrations/` of
  `chassis` and `sinefil`: `hero-home.svg`, `hero-tokens.svg`, `hero-css.svg`, `hero-react.svg`,
  `hero-figma.svg`, `hero-assets.svg` and `hero-icons.svg`. They are of `_default`, so both brands
  have the same files. `Hero.astro` of `@chassis-ui/docs` 0.15 and later inlines them, and
  `chassis.checks.json` checks them after a build. No file is removed or renamed.

### Changed

- Built with `@chassis-ui/assets` 0.12.1, which changes no file. CI pulls the Git LFS files once,
  from a cache, and releases prereleases from `next`.

## [0.5.1]

The web archive of the `docs` app of `sinefil` changes, and the other archives do not. Needs
`@chassis-ui/assets` 0.11.1 to build.

### Changed

- The images of the `docs` app of `sinefil` are drawn, where the files were placeholders of a
  few bytes: in `web/docs/sinefil/images/`, `favicon.svg`, `favicon.png`, `favicon-16x16.png`,
  `favicon-32x32.png`, `apple-touch-icon.png`, `safari-pinned-tab.png`, `social-image.png`,
  `android-chrome-192x192.png`, `android-chrome-512x512.png` and
  `android-chrome-512x512-maskable.png`. The favicon is the logomark of the brand on a gradient of
  its color. No file is added, removed or renamed.
- Built with `@chassis-ui/assets` 0.11.1, which changes no file. CI compiles the iOS and Android
  output of a release with `actool` and `aapt2`.

## [0.5.0]

### Changed

- **Breaking.** The archives are named after the repository:
  `chassis-website-assets-<platform>-<app>-<brand>-<version>.zip` becomes
  `website-assets-<platform>-<app>-<brand>-<version>.zip`. The package is
  `@chassis-ui/website-assets`, and stays private. The content of the archives keeps its paths.
- The app icons of the `demo` app of both brands are redrawn, with a gradient in the background
  of the adaptive icon. @chassis-ui/assets 0.10.0 writes that gradient in
  `res/drawable/app_icon_background.xml`, which 0.9.0 drew black.
- **Breaking.** The layers of the `.icon` bundles of the iOS archives are named by brand, under
  `app-icon/app_icon.icon/Assets/`: `_ chassis-logomark.svg` becomes `chassis-logomark.svg`, and
  `logomark-light.svg` and `logomark-white.svg` of `sinefil` become `sinefil-logomark-dark.svg` and
  `sinefil-logomark-mono.svg`. An app that takes the bundle whole changes nothing.
- Built with `@chassis-ui/assets` 0.10.0.

### Added

- A manifest attached to each release, `website-assets-manifest-<version>.json`, with the size and
  the SHA-256 of every file by job, which `npx chassis-assets diff` compares against.
- This changelog, and `AGENTS.md`. A release takes its text from here, and stops without an entry.

## [0.4.0]

The Android archives change, and the web and iOS archives do not. Needs `@chassis-ui/assets` 0.9.0
to build.

### Changed

- **Breaking.** The fonts move from `fonts/` to `res/font/`, under the same names. The licenses
  stay in `fonts/`.
- **Breaking.** The icons are vector drawables, from `icons/svgs/ic_<name>.svg` to
  `res/drawable/ic_<name>.xml`.
- **Breaking.** The images are in `res/` without their subfolders, and a pair is one resource.
  `images/logo/drawable/logo_light.png` and `logo_dark.png` become `res/drawable-nodpi/logo.png`
  and `res/drawable-night-nodpi/logo.png`, and `images/home/drawable-xhdpi/figma_docs_dark.png`
  becomes `res/drawable-night-xhdpi/figma_docs.png`. An image of one size is in
  `res/drawable-nodpi/`.
- What `res/` does not take stays where it was: the licenses, the SVG images and logos, and
  `icons/icons/ic_chassis_icons.svg`, the sprite of the icons.

### Added

- The app icon: `res/mipmap-anydpi-v26/app_icon.xml`, of
  `res/drawable/app_icon_{background,foreground,monochrome}.xml`, from
  `source/<brand>/demo/app-icon/app-icon.adaptive/`.
- `chassis.checks.json` checks the Android jobs, and the app icon of the iOS jobs.

## [0.3.0]

Needs `@chassis-ui/assets` 0.8.0 to build.

### Changed

- **Breaking.** The logos of `chassis` are one set in `source/chassis/_shared/`.
- A release builds the iOS archives with `Assets.xcassets` and `Icons.xcassets`.
- A release runs on a push to `main` with a new version in `package.json`, in place of a tag
  pushed by hand. The workflow creates the tag `v<version>`, and a push whose version has a tag
  releases nothing.
- The display files of `chassis` are at the weights of the tokens, 400, 500, 600 and 700.

### Added

- A file for every font role and weight in the `demo` app of both brands, which
  `chassis.checks.json` checks on its iOS jobs.
- The app icons of the `demo` app, at `app-icon/app-icon.icon`.

## [0.2.1]

### Added

- The ranges of `chassis.subset` take `cyrillic` and `greek`, for the film titles of sinefil.org:
  both brands get a file per font for each, and a rule per file in `fonts.css`. With the split, a
  page downloads them only for text in those scripts. No file is renamed or removed.

## [0.2.0]

### Changed

- A release builds with `pnpm build:release`: the images are optimized, and the web fonts keep the
  characters of `latin`, `latin-ext`, `symbols2` and the arrows `U+2190-2193`, the union of what
  the Chassis sites set, split by range. One archive of a job serves both the Chassis sites and
  sinefil.org. `pnpm build` stays the plain build.

## [0.1.0]

### Added

- The assets of the Chassis websites and apps, moved from `chassis-ui/assets` with their history:
  `source/` and `chassis.checks.json` of the `chassis` and `sinefil` brands, the `docs` app on the
  web and the `demo` app on iOS and Android.
- One zip per platform, app and brand, attached to each release.
