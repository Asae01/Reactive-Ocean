# Audio Ocean

A 3D audio visualizer that turns a song into a glowing, moving ocean. Built with Three.js and the Web Audio API. No build step, no npm install — just open the HTML file.

![type](https://img.shields.io/badge/type-single--file%20HTML-blue)
![three.js](https://img.shields.io/badge/three.js-r128-black)
![license](https://img.shields.io/badge/license-MIT-green)

## What it does

Drop in an audio file and a wireframe plane turns into an ocean that reacts to the music in real time. Bass hits push the surface up and spawn ripples, treble adds fine surface detail, and the colors shift from deep indigo in the troughs to cyan and then hot pink at the peaks.

- Bass and treble frequencies drive wave height and color
- Beat detection triggers expanding ripple rings
- Orbit camera — drag to rotate, scroll to zoom, auto-rotates when idle
- Drag-and-drop or file picker for loading audio
- Track title/artist parsed from the filename
- Seek bar, volume slider, spacebar to play/pause
- Starfield background for depth

## Getting started

Nothing to install.

1. Download `index.html`
2. Open it in Chrome, Edge, or Firefox
3. Click "Choose a song," or just drag an audio file onto the page

Name your files like `Artist - Title.mp3` if you want the title/artist display to parse correctly.

If playback doesn't start when you open the file directly, some browsers block local file access for audio decoding. Serve it instead:

```
python -m http.server 8000
```
then open `http://localhost:8000/index.html`

## Controls

| Action | Control |
|---|---|
| Rotate camera | Click + drag |
| Zoom | Scroll |
| Play / Pause | Spacebar or button |
| Seek | Drag the progress bar |
| Volume | Slider |
| Load a track | Button, or drag & drop anywhere |

## How it works

The ocean is a `THREE.PlaneGeometry` wireframe. Every frame, each vertex gets pushed up or down based on a few things added together: a constant idle wave so it's never completely still, smoothed bass energy for the big swells, smoothed treble for the finer chop on top, and any active ripple rings from a detected bass hit.

Bass hits are detected by comparing the current bass energy against a rolling average — when it spikes past that, a new ripple spawns.

Vertex colors are calculated from wave height each frame, interpolating indigo → cyan → pink.

Audio analysis uses the Web Audio API's `AnalyserNode`, splitting the frequency spectrum into bass and treble bands.

## Browser support

Needs WebGL and the Web Audio API. Works fine on current Chrome, Firefox, Edge, and Safari.

## License

MIT — use it, modify it, ship it, whatever.
