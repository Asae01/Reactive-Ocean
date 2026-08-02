# 🌊 Audio Ocean

A 3D audio visualizer that turns any song into a glowing, reactive ocean. Built with [Three.js](https://threejs.org/) and the Web Audio API — no build step, no dependencies to install, just open the HTML file in a browser.

![type](https://img.shields.io/badge/type-single--file%20HTML-blue) ![three.js](https://img.shields.io/badge/three.js-r128-black) ![license](https://img.shields.io/badge/license-MIT-green)


## Features

- 🎧 **Real-time audio reactivity** — bass and treble frequencies drive wave height, ripple triggers, and color
- 🌈 **Dynamic color gradient** — deep indigo troughs rise through cyan crests into hot pink peaks
- 💧 **Beat-triggered ripples** — bass hits spawn expanding rings across the grid
- 🖱️ **Orbit camera controls** — drag to rotate, scroll to zoom, gentle auto-rotate when idle
- 📁 **Drag-and-drop or file picker** — load any local audio file
- 🎵 **Track info display** — song title and artist parsed automatically from the filename
- ⏱️ **Seek bar** — scrub to any point in the track
- 🔊 **Volume slider**
- ⌨️ **Spacebar shortcut** — play/pause without touching the mouse
- ✨ **Starfield background** with soft fog for depth

## Getting Started

No installation or build tools required.

1. Download `index.html`
2. Open it in a modern browser (Chrome, Edge, or Firefox recommended)
3. Click **🎵 Choose a song**, or drag an audio file anywhere onto the page

> **Tip:** For the best-looking result, name your files `Artist - Title.mp3` — the app parses this pattern to display a clean track title and artist.

### Run locally with a simple server (optional)

Some browsers restrict local file access for audio decoding. If playback doesn't start, serve the file instead of opening it directly:

```bash
# Python 3
python -m http.server 8000

# then visit
http://localhost:8000/ocean-grid.html
```

## Controls

| Action | Control |
|---|---|
| Rotate camera | Click + drag |
| Zoom | Scroll |
| Play / Pause | Spacebar or button |
| Seek | Drag the progress bar |
| Volume | Volume slider |
| Load a track | Choose a song button, or drag & drop a file anywhere |

## How It Works

- The "ocean" is a `THREE.PlaneGeometry` wireframe whose vertices are displaced vertically each frame based on:
  - an idle ambient wave (so it never sits perfectly still)
  - smoothed bass energy (broad swell)
  - smoothed treble energy (fine surface chop)
  - active ripple rings, spawned when a bass "hit" is detected against a rolling average
- Vertex colors are interpolated per-frame from wave height: dark indigo → cyan → hot pink
- Audio is analyzed with the Web Audio API's `AnalyserNode`, splitting the frequency spectrum into bass and treble bands

## Browser Support

Requires WebGL and the Web Audio API — works in all current versions of Chrome, Firefox, Edge, and Safari.

## License

MIT — free to use, modify, and share.
