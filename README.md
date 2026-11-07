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
| `support.html#rights` | `…/trackprint-webpage/support.html#rights` | The app's Settings ▸ Report a Rights Issue |

The app names these addresses in one place, `TrackPrint/Legal/LegalLinks.swift`
in the app repo, and `MusicBrainzAPI.contact` in its package. If a page is
renamed or the site moves, change those in the same release, and keep the old
address answering until the builds that use it are gone.

## Editing

- `index.html` is the landing page, `style.css` the styles of both pages. Open
  a page in a browser to preview it; there is nothing to install.
- The look follows the app's welcome tour, "Side A". The landing page reads as
  side A of a record, its sections the tracks A1 Welcome, A2 Find, A3 Styles,
  A4 Adjust and A5 Print, each number in its feature's colour: dark is the
  record, light its sleeve, and the record stays black in both. The support
  page is the liner notes, one paper sheet in both themes. Each track is
  centred: its number, headline and line over its content. A3 Styles is a
  reel: the stage holds still under the top bar while you scroll, and each
  poster morphs into the next as its description comes in. With reduced
  motion, or without JavaScript, it is a grid of all eight. The headlines, their
  lines and the features' colours are the app's welcome pages'
  (`TrackPrint/Welcome/WelcomePages.swift`): change one, change both.
- After A5 the record turns over to side B, the players, which the welcome
  tour doesn't have: B1 Now Playing (the eight iPhone players, a reel like
  A3's), B2 Lock Screen (the Live Activity's card and the Dynamic Island),
  B3 Mini Player (a drawn Mac desktop with the mini player at its size in
  points, its size and style chosen under it) and B4 Notch (a drawn MacBook
  screen top whose notch's margin fills as you scroll to it, then opens into
  the player; resting the pointer on it or a tap opens it too). The top bar
  turns with the reader: a Side A / Side B switch, and only that side's
  tracks. Without JavaScript the bar stays on side A, the mini player shows
  Medium in Classic and the notch stays closed. Name only what the shipping
  app does.
- `fonts/` holds Barlow Condensed (headlines) and JetBrains Mono (numbers and
  labels), Latin subsets as WOFF2 under the SIL Open Font License
  (`fonts/OFL.txt`). They are served from this site, so no font service sees a
  visitor; never link a font CDN instead.
- `support.html` holds the questions people ask most, the contact email, a
  section for rights holders and the feedback form. The form posts to the
  same endpoint and contract as the app's Settings ▸ Send Feedback,
  documented in
  [trackprint-feedback](https://github.com/TrackPrint-Music-Posters/trackprint-feedback),
  and the report becomes an issue in the app's private repo. It sends the
  version as `? via website`. The function only answers browsers from this
  site's origin (`https://trackprint-music-posters.github.io`), so the form
  fails from a local preview or if the site moves to another domain: add the
  new origin to `ALLOWED_ORIGINS` in the function first.
- The For rights holders section on `support.html` says what we can do about
  a rights notice and what to send us. The app opens it as
  `support.html#rights` from Settings ▸ Report a Rights Issue, so keep the
  `rights` id even if the heading changes.
- `images/` holds the posters the page shows, one per style, as WebP
  (`cwebp -q 86`), and `og-image.jpg` (1200 × 630) for link previews. The
  albums are **made up**, with generated abstract covers: never put a real
  album's cover on this site, since it is someone else's work. They were drawn
  by TrackPrint's own renderer, from a scratch copy of the `TrackPrintKit`
  package with a small executable target that paints each cover with Core
  Graphics, builds the poster and calls `PosterRenderer`, at scale 0.6
  (1063 × 1417 px). Redraw them when a style's look changes.
  `cover-golden-hour.webp` is the cover of the app's sample album, Golden
  Hour: the label of the hero's record and the cover in Adjust.
- Side B's pictures are screenshots of the app playing the sample album
  (debug builds' `-TrackPrintNowPlayingSample YES`), so no real album shows:
  `player-<style>.webp` and `lock-classic.webp` from the iPhone simulator
  (640 px wide), `island-classic.webp` the Dynamic Island held open, cut
  out on a transparent ground, and from a Mac copy of the app under its own
  bundle id `mini/<style>-<size>.webp` (each window at 2×, captured with
  `screencapture -o -l <window>`, shown at its size in points) and
  `notch-<style>.webp` (the notch player held open on a screen without a
  notch, so its top corners are round; the page squares them off against
  the screen's edge). Take them again when a player's look changes.
- The icons (`icon-512.png`, `apple-touch-icon.png`) are the app icon,
  exported from `TrackPrint/AppIcon.icon` with Icon Composer's `ictool`
  (`--export-image` at 1024 px, macOS rendition for the icon, iOS for the
  touch icon) and scaled with `sips -Z <size>`. `favicon.png` is the app
  icon flattened so it reads at 16 px, without the record's grooves, the
  spindle or the tracklist lines: `favicon.svg`, drawn at 1024 px and scaled
  with `sips -Z 64`. Export them again, and redraw `favicon.svg`, if the app
  icon changes.
- The footer links to the Impressum, privacy policy and terms of use in the
  public
  [trackprint-legal-docs](https://github.com/TrackPrint-Music-Posters/trackprint-legal-docs)
  repo. If those pages move, update the links here too.
- When the app is live, replace the "Coming soon to the App Store" badges
  with the official App Store badge linking to the app's listing.
- `.nojekyll` makes Pages serve the files exactly as committed.
