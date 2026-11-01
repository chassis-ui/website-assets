# Open work

What is left to do, decide or check in this repository, and what was considered and left
out. An entry is removed when it is done. A D-number is a decision of
[docs/decisions.md](https://github.com/chassis-ui/assets/blob/develop/docs/decisions.md) of
chassis-ui/assets, where the assets were kept until 2026-10-29 (D37). Read on 2026-10-29.

## For the maintainer

- **The consumers move to the releases.** Since 0.2.0, a release is built with
  `pnpm build:release`: images optimized, and the web fonts subsetted to `latin`,
  `latin-ext`, `symbols2` and `U+2190-2193`, the union of the ranges the Chassis sites set,
  with `cyrillic` and `greek` since 0.2.1, and split by range. The Chassis sites take the archive of `web/docs/chassis` of a pinned
  release in place of the `vendor/assets` submodule that `chassis-docs vendor` builds, and
  sinefil.org takes the archive of `web/docs/sinefil` from here in place of 0.5.0 of
  chassis-ui/assets. Tracked in chassis-ui/website#33, which adds the release-based vendor
  to `@chassis-ui/docs` and blocks chassis-ui/css#87, chassis-ui/icons#19,
  chassis-ui/figma#14, chassis-ui/react#125 and chassis-ui/tokens#30, and in
  ozgurgunes/sinefil-web#222. Decided on 2026-10-29.
- **The Greek of the `sinefil` fonts.** `chassis.subset.ranges` is one list for both brands,
  and since 0.2.1 it holds `cyrillic` and `greek` for the film titles of sinefil.org. The
  `sinefil` fonts draw Cyrillic, but only a few Greek characters: their `greek` files are
  about 2 KB, so a Greek title still falls back to another font. A family with Greek is the
  maintainer's choice.
- **The `symbols2` files without a glyph.** The split writes a `symbols2` file for the fonts
  that hold only its spaces, with an empty `glyf` table, which Chrome rejects; no page asks
  for one while its text has no box drawing character. The build is to leave such a file
  out: "Not written" in `ref/OPEN.md` of chassis-ui/assets.
- **The logos that the siblings read by their old names.** D33 renamed the logos to
  `images/logo/logo-{black,dark,light,white}.{png,svg}` of each brand, and removed the
  `chassis-{logo,icon}-*` files. Reports for the siblings: `BrandingSection.astro` of
  chassis-ui/website reads `images/logo/chassis-{logo,icon}-{brand,white}-banner.svg` from
  `/static/`, and the table of `packages/docs/README.md` there names them; the pages of
  chassis-ui/css load `images/logo/chassis-logo-brand.svg` with `getStaticPath()` in
  `components/navbar.mdx`, and `about/brand.mdx` loads `chassis-logo-{brand,black,white}.svg`;
  the README of chassis-ui/react shows `https://chassis-ui.com/static/images/logo/chassis-logo-brand.svg`,
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
  says that text keeps its width, which holds for Inter only: a report for chassis-ui/website.
- **The icons of the next `@chassis-ui/icons`.** chassis-ui/icons removed `road-outline-1.svg`
  and `road-solid-1.svg` from its source, export copies of the two icons without the number,
  and its version is `0.4.0-next.0`. The copy in `source/_default/demo/` is the output of 0.3.1
  and has both. A refresh, by the steps of "Refreshing the icons" in `docs/architecture.md`
  of chassis-ui/assets, removes two names from `icons/svgs/` of every job of the `demo` app,
  which is a change of the output.
- **Files an app cannot use.** The apps get the symbol sprite of the icons, since it is an
  SVG, and logos that exist under one name as PNG and as SVG, which meet in one `res/`
  folder or one asset catalog. In the `res/` of a release the PNG is the resource, and the SVG
  stays in `images/logo/drawable/` beside the sprite. The build copies what the source holds,
  and the platform pages say what an app does about each. Removing the copies from
  `source/_default/demo/` is the maintainer's.
- **`--webp` in a release.** Left off: `ref/OPEN.md` of chassis-ui/assets has the numbers.
- **The layers of the Android app icon.** `app-icon.adaptive/` of each brand was drawn from the
  logomark and the fill of its `.icon` bundle on 2026-11-01, and is the designer's to replace.

## Not written

- An entry of `contracts` in `chassis.checks.json` for `fonts/fonts.css`. The sites link the
  stylesheets of `fonts/` from `@chassis-ui/docs` 0.8.0 on, so the entry is due: no check
  fails when it is missing.

## Parked

Considered and left out. Each needs a reason to come back.

- **Removing the `icons/` copy of the `demo` app from `source/`.** Every asset type the pages
  describe is kept, and the icons page describes the copy. The maintainer removed the copy of
  the `docs` app with D33, since the sites take the icons from `@chassis-ui/icons`, and the
  tokens file with D35.
