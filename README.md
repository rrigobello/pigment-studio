# Pigment Studio

A browser-only, brand-independent acrylic paint mixing prototype.

## Features

- Earth and landscape, essential mixing, and expanded studio palettes
- HEX color input and six landscape presets
- Local image upload with click-to-sample color picking
- Deterministic recipes using up to three or four paints
- Reported reference recipes for six landscape presets, shown separately from model estimates
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

The six landscape presets also include reported reference recipes from a supplied image-color comparison. They are shown as separate practical starting points; entries described as “tiny” or “a little” are intentionally approximate and are not used as calibrated model data yet.

## Privacy

Images are processed entirely in the browser and are not uploaded. Saved recipes use this browser's localStorage; they do not sync between devices or domains.

## Source

- index.html — responsive interface and styles
- app.js — default palettes, deterministic optimizer, image sampling, and local storage

There are no external runtime dependencies.
