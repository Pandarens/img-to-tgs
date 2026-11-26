# GIF / Video → Telegram sticker

Static web page that converts GIF, MP4, WEBM into Telegram stickers. Everything runs in the browser, files never leave your device.

Two output modes:
- **TGS** — animated (Lottie) sticker. Vector only, ≤ 64 KB, so frames are vectorized and look stylized.
- **WEBM** — video sticker. VP9 with transparency, 512 px, ≤ 3 s, ≤ 256 KB. Looks like the source.

## How it works
- **TGS:** frames are decoded (`ImageDecoder` / `<video>`), vectorized with imagetracerjs using one shared palette, stacked into Lottie shape layers (512×512, 60 fps) and gzipped. "Auto 64 KB" lowers detail / resolution / FPS until the file fits.
- **WEBM:** frames are encoded with WebCodecs VP9; transparency is encoded as a second VP9 stream and muxed into WebM BlockAdditions (AlphaMode). Bitrate is lowered until the file fits 256 KB.

Needs a recent Chrome, Edge or Firefox.

## Run locally
```
python -m http.server 5173
```
Open http://localhost:5173

## Deploy
Static site, no build step: GitHub Pages (Settings → Pages → branch `main`, root) or `npx vercel`.
