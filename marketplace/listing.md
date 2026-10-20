# Maker Console listing: Now Playing for Feishin

Copy-paste kit for the Elgato Maker Console (https://maker.elgato.com). Values below were
drafted against the Elgato product guidelines (https://docs.elgato.com/guidelines/products)
as researched in October 2026; re-check the guidelines before submitting, because limits can change.

## Product name

Now Playing for Feishin

(23 characters; the limit is 30. "for Feishin" wording marks this as a third-party widget that works alongside the software; it does not use the word "Official" or any Feishin logo. The manifest `name` is "Feishin Now Playing". Note that the widget queries the Navidrome/Subsonic server Feishin points at, not Feishin itself; the description says so. The widget icon is a neutral music-note mark, not the Feishin logo.)

## Tagline

Album art, track details and a recently-added strip from your Navidrome or Subsonic server, on the Xeneon Edge.

(111 characters.)

## Description

Put what is playing on the Xeneon Edge. The widget shows large album art over a blurred copy of the same art, the track title, artist, album, and year with duration, plus an animated equalizer badge and a pulsing Now Playing dot. When nothing is playing it switches to an idle view with your eight most recently added albums. Feishin is a client, so the widget reads your own Navidrome (or any Subsonic-compatible) server directly through the Subsonic API and shows whatever Feishin, or any other client on that server, is playing, with no companion service. A switch limits it to your own plays on a shared server, and sign-in uses Subsonic salted-token authentication so your password is not sent over the network. The art sits on the left in landscape and on top in portrait, every Xeneon Edge slot size is supported, and you can set colors, a background image, glass blur and transparency. Requires iCUE 5.52 or later on Windows, a Xeneon Edge, and a Navidrome or Subsonic server you can reach. This is an independent, unofficial widget, not affiliated with the Feishin project. It is free software under the MIT license, and the source is on GitHub.

(1154 characters; Maker Console asks for 250 to 1500. Counted with Python `len()` on the paragraph above.)

## Category

Audio. (Now-playing display for a music server; the closest observed category is Audio.) The exact Maker Console category list for iCUE widgets was not verified when this kit was
written. The categories observed live on the Elgato Marketplace iCUE widgets page in October 2026 were Audio, Productivity,
Gaming, Artistic, Monitoring, Engagement and Social; pick the closest one the console offers.

## Release notes

Version 1.0.1

- Declares the url network permission in the manifest (`any`, because the server URL is user-entered).
- Sets `min_app_version` to 5.52.
- Bundles the media viewer inside the widget folder and self-closes the head elements, so the package passes the iCUE widget validator.
- Replaces personal host defaults with generic ones.
- Adds a SECURITY policy and a README Install section that points at the GitHub release.

(Condensed from the GitHub release notes for v1.0.1 (`gh release view v1.0.1 -R joshuawowk/icue-widget-feishin`).)

## Requirements

- CORSAIR iCUE 5.52 or later (the manifest sets `min_app_version` to 5.52).
- Windows PC (the manifest targets `os` windows).
- A CORSAIR Xeneon Edge (`dashboard_lcd` device).
- A Navidrome (or other Subsonic-compatible) server reachable from the PC, and a user account on it. A dedicated read-only user works well.
- The server must send CORS headers on `/rest` (Navidrome does by default: `Access-Control-Allow-Origin: *`).
- No companion service is needed.

## Network permissions

The manifest declares one permission: `{ "type": "url", "domain": "any" }`, the iCUE spec's wildcard for all external hosts. It is needed because the Navidrome Server URL is whatever the user types. The widget talks only to that server; credentials are stored in iCUE widget settings and authentication uses Subsonic salted tokens. The wildcard does not cover `localhost`: if Navidrome runs on the same PC, iCUE asks for permission at runtime and the user clicks Allow. iCUE shows the permission at install, and it can be revoked in the widget settings.

## License

MIT, see `LICENSE` in the repository root. Source: https://github.com/joshuawowk/icue-widget-feishin

## Submission notes

- Asset specification unverified. The iCUE-specific listing asset requirements (icon size, gallery image count and
  dimensions, description limits) were not found in Elgato's documentation when this kit was written. This kit reuses the
  sizes of the Stream Deck kit: a 288x288 listing icon and 1920x960 gallery images, with a description of 250 to 1500
  characters. Re-check the Maker Console form and resize or re-render (`marketplace/build.sh`) if it asks for something else.
- Submission route unverified. Elgato's become-a-maker page lists Stream Deck, Wave Link, OBS and 3D as self-serve Maker
  Console categories but does not list iCUE widgets. If the console has no iCUE widget option, the fallback is the
  maker@elgato.com "New Product Submission" email route.
- File to upload: `feishin-now-playing.icuewidget`, the `.icuewidget` attached to GitHub release v1.0.1:
  https://github.com/joshuawowk/icue-widget-feishin/releases/download/v1.0.1/feishin-now-playing.icuewidget
  Download it from the release; do not zip the folder by hand. To rebuild it, use `npm run package` (needs
  `npm install -g icuewidget-cli`).
- Manifest version is 1.0.1 and the file above matches release v1.0.1. If you submit a later release, update the
  version, release notes and file name in this kit first.
- Listing icon: `resources/icon.png` is 256x256 and was upscaled to 288x288 with ImageMagick (`convert resources/icon.png -resize 288x288!`), so it is slightly soft; re-export `resources/icon.svg` at 288 for a sharper icon if needed.
- Packaging caveat: `npm run package` runs `icuewidget package .` on the repository root, which zips every non-hidden file. A `marketplace/` folder would therefore be swept into future `.icuewidget` builds (about 0.8 MB of PNGs and HTML). Nothing in this kit changes the package script; stage the widget files or exclude `marketplace/` before the next release build.
- Validator note: `icuewidget validate` (CLI 0.5.0, run in October 2026 on the unzipped local `dist/` build of that version) passes with one warning that the `any` url permission grants access to every external host. The permission is intentional because the host is user-entered; expect reviewers to ask about it and point them at the Network permissions section.
- Not tested on hardware: the kit was written without Windows, iCUE or a Xeneon Edge. Gallery slides show the shipped preview and text only; no screenshot was taken from a running panel.

## Assets in this folder

| File | Size | Use |
| --- | --- | --- |
| `listing-icon-288.png` | 288x288 | Product icon |
| `gallery-01.png` | 1920x960 | Overview: product name and the widget preview (`resources/preview.png`) |
| `gallery-02.png` | 1920x960 | Feature cards: now playing, backdrop, idle view, filters, auth, sizing |
| `gallery-03.png` | 1920x960 | Connection to the Navidrome server, setup steps and network permission |

Slide 1 shows the widget's own `resources/preview.png` unmodified. It displays a sample track title and artist over a generated gradient, not real cover art. Those names are third-party factual metadata used as sample text; swap the preview if you would rather not show them.
`marketplace/src/` holds the HTML sources and `marketplace/build.sh` re-renders the gallery PNGs with
headless Chromium.

## Trademark note

"Feishin" is the name of a separate open-source project and "Navidrome" is a separate open-source server. This widget is independent and unofficial, and uses neither logo.
