# Spotilol - v1.1.6.1 (09.29.2026)

Fork release based on [upstream v1.1.6](https://github.com/lyssadev/Spotilol/releases/tag/1.1.6), plus faster startup and cache reuse (proposed upstream in [lyssadev/Spotilol#97](https://github.com/lyssadev/Spotilol/pull/97)).

## v1.1.6.1 Changelog

### performance
- **no more double-fetching** — in normal (non-proxy) mode every WebView request was fetched twice (once natively, then again by the WebView). Only ad-audio candidates and Google auth URLs are sniffed natively now; everything else goes straight to the WebView
- **HTTP cache kept across launches** — the web player bundle is no longer wiped on every close, so repeat cold starts load from disk. Manual "Clear cache" / "Clear all data" in settings still work
- **faster splash** — removed fixed delays (~3.1s saved in normal mode); proxy mode waits for the proxy to bind instead of sleeping; exit fade shortened from 500ms to 150ms; Firebase Analytics/Performance init moved off the main thread
- **early injections run at document start** — on `open.spotify.com` the spoof/ad/power-save payload is registered as a document-start script so it runs before Spotify's own scripts, with the old injection kept as a fallback for older System WebView versions and other origins

### fixed
- **power save video freezing** — the video observer now attaches even when `document.body` doesn't exist yet (it previously failed silently)

## install notes
- signed with this fork's own key, which differs from upstream. If the upstream app is installed, uninstall it first.
- signing certificate SHA-256: `38:69:B6:B9:B2:48:70:E5:3B:04:E5:7A:CA:CD:1B:3D:B5:6F:4D:18:96:D3:99:CB:F2:A2:46:00:20:F7:FB:1E`
- built without Firebase config, so analytics and crash reporting are off.
