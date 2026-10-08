# darachPhotography — AR Dancer

Scan a QR code → the kneeling swan dancer from the darachPhotography logo appears in your room, with the client's lightning bolt striking down the screen.

Built on Google's `<model-viewer>`, so it works with no app install:

| Device | What happens when "View in your space" is tapped |
|---|---|
| Android (Chrome) | WebXR AR in the browser — lightning strikes as the dancer is placed on the floor |
| Android (fallback) | Google Scene Viewer |
| iPhone / iPad | Apple AR Quick Look (needs `dancer.usdz`, see below) |
| Desktop | 3D preview you can spin, plus a note to open on a phone |

## 1. The dancer model (included)

`models/dancer.glb` (Android + desktop) and `models/dancer.usdz` (iPhone) are already prepared from the Meshy export:

- **Real-world size:** about 1.05 m across the tutu, 0.49 m tall, 0.68 m wide. That is life-size for a dancer kneeling and folded forward.
- **Placement:** her feet sit exactly on the floor (y = 0) and she's centred on the spot where the viewer taps. She faces the viewer.
- **Optimised for phones:** simplified from 751k to 110k triangles, with textures resized (base colour 2048 px, normal and roughness maps 1024 px). The GLB is 4.1 MB (from 26 MB) and the USDZ is 8.3 MB (from 30 MB), with no visible loss of detail.

**To change her size**, edit `scale` in `index.html`'s `<model-viewer>` tag, e.g. `scale="1.2 1.2 1.2"` for 20% bigger. This affects the in-page view and Android AR. iPhone AR always uses the USDZ's built-in size, and people can pinch to resize her in AR on both platforms.

## 2. Publish on GitHub Pages

1. Create a new repository (e.g. `darach-ar`) and upload everything in this folder, keeping the structure.
2. Repo **Settings → Pages → Source: Deploy from a branch → `main` / `(root)`** → Save.
3. After a minute your site is at `https://<your-username>.github.io/darach-ar/`.

AR requires HTTPS — GitHub Pages provides it automatically.

## 3. Get the QR code

Open `https://<your-username>.github.io/darach-ar/qr.html`. It generates a QR code pointing at the live AR page; tap **Download PNG** for print. It uses high error-correction, so it survives printing small or on textured stock (keep it at least 2 × 2 cm).

## The lightning bolt

A procedurally generated bolt (different every strike) cracks down through the wordmark toward the dancer, with a screen flash:
- when the model first loads,
- every 6–11 seconds while viewing,
- the moment she's placed in the room (Android WebXR).

Run `strike()` in the browser console to trigger it on demand. It's switched off for anyone with "reduce motion" enabled.

**iPhone note:** Apple Quick Look runs AR in a separate system viewer, so web effects can't be drawn there. To have lightning *inside* iOS AR it would need to be baked into the 3D model as an animation (e.g. a bolt mesh animated in Blender, exported in the USDZ).

## Files

```
index.html        AR experience
qr.html           QR code generator for the live URL
assets/logo.jpg   logo, used as the loading poster
models/           put dancer.glb + dancer.usdz here
```
