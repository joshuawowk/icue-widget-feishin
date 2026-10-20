# Feishin Now Playing — iCUE Widget for Xeneon Edge

[![Release](https://img.shields.io/github/v/release/joshuawowk/icue-widget-feishin)](https://github.com/joshuawowk/icue-widget-feishin/releases/latest)
[![License: MIT](https://img.shields.io/github/license/joshuawowk/icue-widget-feishin)](LICENSE)

A now-playing widget for **Feishin / Navidrome** on the CORSAIR Xeneon Edge: big album art with a blurred art backdrop, track / artist / album, an animated EQ badge, and a recently-added strip when nothing is playing.

![preview](resources/preview.png)

Feishin is a client — the listening data lives on the **Navidrome** (or any Subsonic-compatible) server it points at. This widget queries that server directly via the Subsonic API (`getNowPlaying`), so it shows whatever Feishin (or any other client) is scrobbling, with zero companion services.

## Features

- **Now playing**: album art, title (2-line clamp), artist, album, year • duration • freshness
- Blurred album-art backdrop for an ambient look
- Animated EQ bars overlay + pulsing NOW PLAYING dot
- **Idle state**: "Nothing playing" with your 8 most recently added albums
- "Only My Plays" switch to ignore other users on a shared server
- Subsonic **salted-token auth** (`t = md5(password + salt)`) — your password is never sent
- Responsive: art-left on landscape, art-top on portrait, all Edge slot sizes
- Personalization: colors, background image, glass blur, transparency

## Install

**Prerequisites**

- Windows PC with CORSAIR iCUE 5.52 or newer and a Xeneon Edge
- Your own **Navidrome** (or other Subsonic-compatible) server reachable from the PC, plus a user account on it
- The server must send CORS headers on `/rest` (Navidrome does by default: `Access-Control-Allow-Origin: *`)

**Steps**

1. Download `feishin-now-playing.icuewidget` from the [latest release](https://github.com/joshuawowk/icue-widget-feishin/releases/latest).
2. Double-click the file, or in iCUE open **Widgets**, click **+**, and select the file.
3. Add the widget to a Xeneon Edge slot and open its settings:
   - **Navidrome Server URL** (e.g. `https://navidrome.example.com`)
   - **Username** / **Password** (a dedicated read-only Navidrome user works great)

**Network permission.** Because the server URL is whatever you type, the manifest declares `{ "type": "url", "domain": "any" }` (the spec's wildcard for all external hosts). iCUE shows this at install and you can revoke it in the widget settings. The wildcard does not cover `localhost`; if Navidrome runs on the same PC, iCUE will ask for permission at runtime, so click Allow.

## Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| Navidrome Server URL | text | — | Your server, HTTPS recommended |
| Username / Password | text | — | Subsonic credentials |
| Only My Plays | switch | on | Filter `getNowPlaying` to your user |
| Refresh Interval | slider | 10 s | 5–60 s |
| Text / Accent / Background Color | color | white / `#22d3ee` / `#15161c` | |
| Background Image + Glass Blur | media | — | Shown behind the art backdrop |
| Background Transparency | slider | 100% | |

## States

Connecting · Setup (missing credentials) · Now playing · Idle (recently added) · Error (bad credentials / unreachable)

## Privacy

Talks only to the server you configure. Credentials live in iCUE widget settings; auth uses Subsonic salted tokens so the raw password never crosses the wire.

## Development

Requires Node.js and the official CLI (`npm install -g icuewidget-cli`, tested with 0.5.0).

```bash
npm run validate   # icuewidget validate .
npm run package    # icuewidget package . -o dist/feishin-now-playing.icuewidget
```

Always build the package with `icuewidget package` (it validates first); do not zip the folder by hand. `dist/` is gitignored.

## License

MIT
