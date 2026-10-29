# Open work

What is left to do, decide or check in this repository, and what was considered and left
out. An entry is removed when it is done. A D-number is a decision of
[docs/decisions.md](https://github.com/chassis-ui/assets/blob/develop/docs/decisions.md) of
chassis-ui/assets, where the assets were kept until 2026-10-29 (D37). Read on 2026-10-29.

## For the maintainer

- **The first release.** The version is 0.1.0, a new sequence: the assets were released as
  0.5.0 of chassis-ui/assets last. A release is a tag, `v<version>`, and the archives are
  named `chassis-website-assets-<platform>-<app>-<brand>-<version>.zip`, where sinefil.org
  read `chassis-assets-web-docs-sinefil-<version>.zip`: sinefil.org takes the new name from
  the first release. The CI of this repository installs `@chassis-ui/assets` from npm, so it
  passes once 0.6.0 is published.
- **`chassis-docs vendor` of `@chassis-ui/docs`.** When a site subsets fonts, it installs
  the submodule with `pnpm install --filter @chassis-ui/assets --prod`, a filter of the old
  workspace. Here the build is a dependency, so `pnpm install --prod` is enough, and the
  filter matches no project. A report for chassis-website, due when the sites move their
  submodule to this repository.
- **The weights of the `display` role of the `chassis` brand.** Its Montserrat files, taken
  from `feat/new-chassis-brand` on 2026-10-19, are at 300, 400, 600 and 700, the weights of
  the `ui` role, while `typography.fontWeight.display` of `source/brand-chassis/brand-base.json`
  in chassis-tokens 0.10 is Regular, Medium, SemiBold and Bold, 400, 500, 600 and 700. The
  files by weight of `elegant` and `normal`, and the comment of `fonts.css`, follow one of the
  two once the maintainer says which.
- **The logos that the siblings read by their old names.** D33 renamed the logos to
  `images/logo/logo-{black,dark,light,white}.{png,svg}` of each brand, and removed the
  `chassis-{logo,icon}-*` files. Reports for the siblings: `BrandingSection.astro` of
  chassis-website reads `images/logo/chassis-{logo,icon}-{brand,white}-banner.svg` from
  `/static/`, and the table of `packages/docs/README.md` there names them; the pages of
  chassis-css load `images/logo/chassis-logo-brand.svg` with `getStaticPath()` in
  `components/navbar.mdx`, and `about/brand.mdx` loads `chassis-logo-{brand,black,white}.svg`;
  the README of chassis-react shows `https://chassis-ui.com/static/images/logo/chassis-logo-brand.svg`,
  which stops working when the website deploys this version. The entry of `contracts` in
  `chassis.checks.json` for the website's logos was removed with D33: add the names the
  website reads once it reads the new ones.
- **The choices of D28.** Two were the session's: Inter is at the optical size 14 in every
  file by weight, so the app fonts left the 18pt cut of D24, and `code-strong` of the default
  brand is the Bold, 700. Both are in 0.3.0 of chassis-ui/assets and wait for a confirmation.
- **The code font of the pages is wider than it was.** Fira Code 6.2 of `source/` has an
  advance of 1200 in an em of 1950, 0.6154 em, where the 5.002 of Google Fonts, which the
  pages loaded up to `@chassis-ui/docs` 0.7, has 0.6 em: code is 2.56% wider on every site
  that moves to 0.8.0. Measured on the assets site on 2026-10-12, at 375 and 1280 pixels:
  code blocks scroll that much further, 94 of 16,135 pieces of text wrap on another line,
  and a page is 0.02% to 1.02% taller. Inter has the same width at every size and weight.
  D28 chose the family, and `docs/fonts.md` names its other line metrics, not the width. To
  keep the old width, a `size-adjust` of 97.5% in `fonts.css` or the 5.002 files would do
  it, and both change `source/`. "From 0.7 to 0.8" of `UPGRADING.md` of `@chassis-ui/docs`
  says that text keeps its width, which holds for Inter only: a report for chassis-website.
- **The icons of the next `@chassis-ui/icons`.** `chassis-icons` removed `road-outline-1.svg`
  and `road-solid-1.svg` from its source, export copies of the two icons without the number,
  and its version is `0.4.0-next.0`. The copy in `source/_default/demo/` is the output of 0.3.1
  and has both. A refresh, by the steps of "Refreshing the icons" in `docs/architecture.md`
  of chassis-ui/assets, removes two names from `icons/svgs/` of every job of the `demo` app,
  which is a change of the output.
- **Files an app cannot use.** The apps get the symbol sprite of the icons, since it is an
  SVG, and logos that exist under one name as PNG and as SVG, which meet in one `res/`
  folder or one asset catalog. The build copies what the source holds, and the platform
  pages say what an app does about each. Removing the copies from `source/_default/demo/` is
  the maintainer's.

## Not written

- An entry of `contracts` in `chassis.checks.json` for `fonts/fonts.css`. The sites link the
  stylesheets of `fonts/` from `@chassis-ui/docs` 0.8.0 on, so the entry is due: no check
  fails when it is missing.
- A test of `build/instance-font.py`. It is Python, and the repository has no runner for it.

## Parked

Considered and left out. Each needs a reason to come back.

- **Removing the `icons/` copy of the `demo` app from `source/`.** Every asset type the pages
  describe is kept, and the icons page describes the copy. The maintainer removed the copy of
  the `docs` app with D33, since the sites take the icons from `@chassis-ui/icons`, and the
  tokens file with D35.
