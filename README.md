# Object Detection in HTML Canvas

A small JavaScript project that detects color-based regions on an image drawn to an HTML `<canvas>`, then calculates and logs the center point of each detected region.

This project is currently focused on detecting "available seat" markers (green-ish color range) from a source image.

## Project Purpose

This project demonstrates a simple computer-vision style approach in the browser using raw pixel data:

- Read image pixels from a canvas (`getImageData`)
- Filter pixels by RGB color thresholds
- Group connected pixels into regions
- Compute the center of each region

It is useful as a starting point for tasks like:

- Seat detection in ticket maps
- Marker/shape localization on static images
- Basic color segmentation in frontend-only apps

## Current Features

- Loads an image and draws it to a canvas
- Scans all pixels to find a target color range
- Clusters neighboring matching pixels using BFS
- Calculates and prints center coordinates for each cluster
- Logs detected matching pixels and final centers in the browser console

## Project Structure

```text
objectDetectInHtmlCanvas/
├─ index.html    # Main app (HTML + JS logic)
└─ README.md
```

## How It Works

1. The image (`#source`) is loaded and drawn onto `#myCanvas`.
2. `detectGreenRectsCenters(canvas)` loops through RGBA data.
3. Pixels inside the configured RGB threshold are collected.
4. `groupGreenRegionsAndFindCenters(...)` groups connected pixels (4-directional).
5. The center of each group is calculated by averaging X/Y coordinates.
6. The resulting centers are rounded and logged.

## Requirements

- A modern web browser (Chrome, Edge, Firefox, etc.)
- Project files on your local machine
- A source image file referenced in `index.html` (currently `./3.png`)

## Run Locally

Because browsers may restrict local file access (`file://`) for canvas/image workflows, it is recommended to run via a simple local server.

### Option 1: VS Code / Cursor Live Server

1. Open the project folder.
2. Run **Live Server** on `index.html`.
3. Open the page in your browser.
4. Open DevTools Console to inspect output.

### Option 2: Python HTTP Server

```bash
python -m http.server 8000
```

Then open:

[http://localhost:8000](http://localhost:8000)

## Configuration

The target color range is configured inside `index.html`:

- `r` (red) range
- `g` (green) range
- `b` (blue) range

Adjust those thresholds to detect different seat states or marker colors in your images.

## Example Output

In the browser console:

- `greenPixels: [...]` -> all pixels matching the target color
- `Centers of green rectangles: [{ x: ..., y: ... }, ...]` -> detected region centers

## Sample Screenshots

The following screenshots are included to help visitors quickly understand the input/output visuals of this project:

### Screenshot 1

![Screenshot 1](./1.png)

### Screenshot 2

![Screenshot 2](./2.png)

### Screenshot 3

![Screenshot 3](./3.png)

### Screenshot 4

![Screenshot 4](./4.png)

### Screenshot 5

![Screenshot 5](./5.png)

## Limitations (Current Version)

- Detection is based only on fixed RGB thresholds
- Sensitive to color variations, shadows, and anti-aliasing
- Uses linear pixel lookups (`find`) during BFS, which can be slow for large images
- Single-file prototype (logic is embedded in `index.html`)

## Possible Improvements

- Move JavaScript into separate modules/files
- Use a `Set`/map for faster pixel membership checks
- Add region size filtering (ignore tiny noisy clusters)
- Draw detected centers visually on the canvas
- Add configurable UI sliders for RGB thresholds
- Support multiple seat-state color profiles

## License

No license file is included yet.  
If you plan to publish this publicly, consider adding a license such as MIT.

