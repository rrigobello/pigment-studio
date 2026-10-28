# Pigment Studio

A browser-only, brand-independent acrylic paint mixing prototype.

## Features

- Earth and landscape, essential mixing, and expanded studio palettes
- HEX color input and six landscape presets
- Local image upload with click-to-sample color picking
- Deterministic recipes using up to three or four paints
- Reported reference recipes for six landscape presets, shown separately from model estimates and surfaced for nearby sampled colors
- Locally saved personal reference anchors for recipes confirmed against dried swatches
- Browser-only export/import for moving saved recipes and personal anchors between devices
- Qualitative practical recipe families for earth, olive, neutral, red, blue, violet, and ochre targets
- Predicted color comparison, clipboard copying, and local recipe history

## Run locally

Serve this directory with any static HTTP server, for example:

```sh
python3 -m http.server 8000
```

Open http://localhost:8000. No installation, API keys, backend, or build step required.

## GitHub Pages

In repository Settings → Pages, choose **Deploy from a branch**, select **main** and **/(root)**, then save. The root contains index.html, app.js, and .nojekyll.

## Model and limitations

Generic paint colors are converted from sRGB to linear RGB, then into three-channel absorption-to-scattering estimates. Candidate mixtures are reconstructed using a Kubelka–Munk-inspired approximation and compared to the target in Oklab. This is an approximation, not a spectral pigment simulation.

The search exhaustively checks a fixed 5% proportion grid with a stable paint order and deterministic tie handling. The same inputs and settings yield the same recipe.

These generic swatches are **not calibrated against real acrylic paints**. The model does not account for measured spectra, tinting strength, brands, drying, film thickness, substrate, lighting, or metamerism. Model percentages are not validated weight or volume formulas. Treat recipes as starting estimates, use approximate equal-sized parts for a small test, and assess dried swatches under consistent lighting before mixing larger quantities.

The six landscape presets also include reported reference recipes from a supplied image-color comparison. They are shown as separate practical starting points; nearby sampled colors may surface the closest reported anchor, but entries described as “tiny” or “a little” are intentionally approximate and are not used as calibrated model data yet. For colors without a nearby reference, the app now shows a qualitative practical recipe family based on general pigment behavior—for example, Yellow Ochre + Ultramarine + Raw Umber for muted olives—alongside the mathematical model estimate. If you have a recipe confirmed against a dried swatch, the **Add a tested recipe** panel stores it locally as a personal reference anchor for future nearby samples. Personal anchors are empirical notes, not a recalibration of the model.

## Privacy

Images are processed entirely in the browser and are not uploaded. Saved recipes and personal anchors use this browser's localStorage; they do not sync automatically between devices or domains. Use the local data export/import controls to move a JSON backup manually.

## Source

- index.html — responsive interface and styles
- app.js — default palettes, deterministic optimizer, image sampling, and local storage

There are no external runtime dependencies.
