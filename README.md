[README-1.md](https://github.com/user-attachments/files/32156995/README-1.md)
# Bridge — DIY AR artwork tool

A single-file web app that:
1. Takes an uploaded image (the "marker" — the artwork someone points a camera at)
2. Compiles it into a trackable AR target **in the browser** (no server, no build step)
3. Opens the device's regular camera and overlays an uploaded video on top of the artwork whenever it's recognized

Built on [MindAR](https://hiukim.github.io/mind-ar-js-doc/) (image tracking) and [three.js](https://threejs.org/) (rendering), both loaded from a CDN.

# Bridge — DIY AR artwork tool

A single-file web app that:
1. Lets you build a **gallery** of artworks — each with its own trigger image and overlay video
2. Compiles them into trackable AR targets **in the browser** (no server, no build step)
3. Opens the device's regular camera and recognizes *any* piece in your gallery, overlaying its video whenever that artwork is in frame
4. Lets you **export your gallery as a file** to share it with someone else, or move it to another device

Built on [MindAR](https://hiukim.github.io/mind-ar-js-doc/) (image tracking) and [three.js](https://threejs.org/) (rendering), both loaded from a CDN.

## Running it

Camera access requires a **secure context** — `https://` or `localhost`. Opening `index.html` directly with `file://` will not get camera permission in most browsers.

Easiest options:

- **Local testing:** from this folder, run `npx serve .` (or `python3 -m http.server 8000`) and visit `http://localhost:PORT`.
- **Quick public hosting:** drag the `ar-artwork-tool` folder onto [Netlify Drop](https://app.netlify.com/drop), or push it to a GitHub repo and enable **GitHub Pages**. Both give you free HTTPS automatically.
- **On a phone:** once it's hosted with HTTPS, open the URL directly in mobile Safari or Chrome — no app install needed.

## Using it

1. From the gallery, tap **+ Add artwork**. Give it a name, an image with good detail/contrast/texture, and the video that should play over it.
2. Repeat for as many pieces as you want — they all live in the same gallery.
3. Tap **Open AR camera** to scan for *all* of them at once (the camera recognizes whichever one it sees), or **Scan just this** on a single card to test one piece on its own.
4. Point the camera at a printed or displayed copy of an artwork. Its video locks onto it, and pauses when that artwork leaves frame. Up to 4 pieces can be tracked simultaneously in one session.

## Sharing a gallery (export / import)

There's no cloud account behind this — everything lives in that browser's local storage. To hand a gallery to someone else, or move it to another device:

1. Tap **Export library** — downloads a single `bridge-library.json` file containing every image and video, bundled together.
2. Send that file however you'd send any file (email, AirDrop, a shared drive).
3. On the receiving end, open this same tool and tap **Import library**, then pick the file. Its artworks get added alongside whatever's already there.

Keep in mind the export embeds full video files as text, so a library with long or high-resolution videos can produce a large file — short, compressed clips travel best.

## Notes & limits

- Everything happens client-side — no files are uploaded anywhere unless you explicitly export and send a library file yourself.
- Your gallery is saved in the browser's IndexedDB, on that device, in that browser. Closing the tab or restarting the device doesn't lose it; a different browser or device won't see it (use export/import to move it), and clearing site data / browsing data will remove it.
- Tracking quality depends entirely on the source images. If tracking feels jittery or an artwork won't recognize, try a higher-resolution or higher-contrast photo.
- iOS Safari requires video to start muted (handled already) — you can add an unmute button if sound matters.
- Pinned to `mind-ar@1.2.5` and `three@0.132.2` via CDN for stability. Newer versions may have API changes.

