# Luben Streetball 1vs1 · Booth filters

The video booth for the touch screen at the Luben Streetball 1vs1 event (Σάββατο 14/11/2026). The screen is vertical and has a camera on top. The booth runs in the browser and needs **no GPU**: everything runs on the CPU.

**Live:** https://stavrosvikas.github.io/luben-streetball-booth/

## Flow
1. **Idle screen**: the logo sits top-left, «ΘΕΛΕΙΣ ΝΑ ΓΙΝΕΙΣ VIRAL ΠΡΟΦΑΝΩΣ» runs across the middle and the filters sit at the bottom.
2. The guest picks a filter and presses **ΠΑΜΕ**. A 3-2-1 countdown runs, then the camera records for 3 seconds.
3. The clip is processed, then plays as a loop. A QR code sits top-left and the logo is burned into the video, bottom-centre.

## Filters
| Filter | What it does | Matting |
|---|---|---|
| Ghost Echo | Magenta silhouettes trail behind the player over a B&W background (approved look, `ghost-echo-v1-LOCKED.html`) | RVM |
| Earthquake Echo | Freeze frame. The background turns magenta, the black balls pop in and the whole picture shakes and echoes | RVM |
| RGB Ghost | 4× smooth slow motion with magenta and red full-frame ghosts | none |
| Jittery Sticker | Colour video; at the hit the background goes B&W and the player jitters as a sticker | RVM |
| Flame Outline | The player is engulfed in procedural fire (brand or natural colours) | RVM |
| Player Card | Freeze on a still pose; a card builds around it with a court texture from the animation, magenta graphics, the player again huge behind, the logo and «KING OF THE COURT?» | RVM |

## Tech
- Matting uses **Robust Video Matting** (MobileNetV3, ONNX). It runs through onnxruntime-web on WASM/CPU. The model is in `rvm_model.js`, base64-encoded so it also works from `file://`.
- The fire is procedural: domain-warped noise, no stock footage.
- **S** key: opens the operator panel (camera rotation, capture length, freeze, intensity, fire colour).
- `booth-v3.html?auto=quake`: test hook that picks a filter and starts recording on its own.

## Not done yet
- The QR is a **placeholder**. The video has to be uploaded to the booth server, and the QR has to point to the link the server returns.
