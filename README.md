# 🐼 Panda Stickers — GIF / видео → стикер Telegram

**[Открыть конвертер](https://pandarens.github.io/img-to-tgs/)** · [English](#english)

Статическая страница: превращает GIF, MP4, WEBM в стикеры Telegram. Всё работает в браузере, файлы никуда не загружаются. Интерфейс на русском и английском. Можно закинуть сразу много файлов: они конвертируются по очереди, каждый скачивается отдельно или все разом одним ZIP.

Удобства: вставка из буфера (Ctrl+V), пресеты качества, превью на фоне чата Telegram, светлая и тёмная тема, настройки запоминаются, инструкция как добавить стикер через @Stickers.

Два режима:
- **TGS**: анимированный (Lottie) стикер. Только векторы, ≤ 64 КБ, поэтому кадры векторизуются и выглядят стилизованно.
- **WEBM**: видеостикер. VP9 с прозрачностью, 512 px, ≤ 3 с, ≤ 256 КБ. Выглядит как исходник.

## Как это работает
- **TGS:** кадры декодируются (`ImageDecoder` / `<video>`), векторизуются imagetracerjs с общей палитрой, складываются в слои Lottie (512×512, 60 fps) и сжимаются gzip. «Автоматически ужать до 64 КБ» снижает детализацию, разрешение и FPS, пока файл не влезет.
- **WEBM:** кадры кодируются WebCodecs в VP9; прозрачность кодируется вторым VP9-потоком и записывается в BlockAdditions (AlphaMode). Битрейт снижается, пока файл не влезет в 256 КБ.

Нужен свежий Chrome, Edge или Firefox.

## Запуск локально
```
python -m http.server 5173
```
Открыть http://localhost:5173

## Деплой
Статический сайт без сборки: GitHub Pages (Settings → Pages → ветка `main`, корень) или `npx vercel`.

---

<a id="english"></a>
# 🐼 Panda Stickers — GIF / video → Telegram sticker

**[Open the converter](https://pandarens.github.io/img-to-tgs/)** · [Русский](#-panda-stickers--gif--видео--стикер-telegram)

Static web page that converts GIF, MP4, WEBM into Telegram stickers. Everything runs in the browser, files never leave your device. The interface is in Russian and English. Drop many files at once: they are converted one by one, download each separately or all of them as one ZIP.

Extras: paste from clipboard (Ctrl+V), quality presets, preview on a Telegram-chat background, light and dark theme, settings are remembered, a how-to for adding stickers via @Stickers.

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
