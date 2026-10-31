# TrackPrint website

The page for TrackPrint, the album poster app for iPhone, iPad and Mac: a
landing page, a support page with the feedback form, and their stylesheet.
Static HTML, no build step.

## Published at

GitHub Pages serves `main` from the repo root:
<https://trackprint-music-posters.github.io/trackprint-webpage/>

| Page | Address | Used as |
|---|---|---|
| `index.html` | `…/trackprint-webpage/` | Marketing URL in App Store Connect |
| `support.html` | `…/trackprint-webpage/support.html` | Support URL in App Store Connect, the app's Settings ▸ Support, and the MusicBrainz User-Agent contact |

The app names both addresses in one place, `TrackPrint/Legal/LegalLinks.swift`
in the app repo, and `MusicBrainzAPI.contact` in its package. If a page is
renamed or the site moves, change those in the same release, and keep the old
address answering until the builds that use it are gone.

## Editing

- `index.html` is the landing page, `style.css` the styles of both pages. Open
  a page in a browser to preview it; there is nothing to install.
- `support.html` holds the questions people ask most, the contact email and
  the feedback form. The form posts to the same endpoint and contract as the
  app's Settings ▸ Send Feedback, documented in
  [trackprint-feedback](https://github.com/TrackPrint-Music-Posters/trackprint-feedback),
  and the report becomes an issue in the app's private repo. It sends the
  version as `? via website`. The function only answers browsers from this
  site's origin (`https://trackprint-music-posters.github.io`), so the form
  fails from a local preview or if the site moves to another domain: add the
  new origin to `ALLOWED_ORIGINS` in the function first.
- `images/` holds the posters the page shows, one per style, as WebP
  (`cwebp -q 86`), and `og-image.jpg` (1200 × 630) for link previews. The
  albums are **made up**, with generated abstract covers: never put a real
  album's cover on this site, since it is someone else's work. They were drawn
  by TrackPrint's own renderer, from a scratch copy of the `TrackPrintKit`
  package with a small executable target that paints each cover with Core
  Graphics, builds the poster and calls `PosterRenderer`, at scale 0.6
  (1063 × 1417 px). Redraw them when a style's look changes.
- The icons (`icon-512.png`, `apple-touch-icon.png`, `favicon.png`) are the
  app icon, exported from `TrackPrint/AppIcon.icon` with Icon Composer's
  `ictool` (`--export-image`, macOS rendition for the icon and favicon, iOS
  for the touch icon) and scaled with `sips -Z <size>`. Export them again if
  the app icon changes.
- The footer links to the Impressum, privacy policy and terms of use in the
  public
  [trackprint-legal-docs](https://github.com/TrackPrint-Music-Posters/trackprint-legal-docs)
  repo. If those pages move, update the links here too.
- When the app is live, replace the "Coming soon to the App Store" badges
  with the official App Store badge linking to the app's listing.
- `.nojekyll` makes Pages serve the files exactly as committed.
