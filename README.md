# model-viewer GitHub Pages starter

This repo is a tiny, no-build static site for testing `glTF/GLB` models with
[`<model-viewer>`](https://modelviewer.dev/). Drop a `model.glb` into `assets/`,
push to GitHub, and GitHub Pages will host it.

## Quick start
1. Copy this folder into a new GitHub repo (e.g., `c4d-model-viewer-test`).
2. In **Settings → Pages**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, then **Save**.
3. Put your model file at `assets/model.glb`. Keep it under ~100 MB.
4. (Optional) Add an environment map at `assets/environment.hdr`.
5. Visit `https://<your-username>.github.io/<repo-name>/`.

> Note: GitHub Pages does **not** serve Git LFS objects. Keep the GLB small via Draco/meshopt and texture compression. 

## Converting C4D (Redshift) → GLB (via Blender)
**In Cinema 4D (Redshift):**
- Bake PBR textures for each material: Base Color (sRGB), Roughness (non-color), Metallic (non-color), Normal (tangent, non-color), Emissive (sRGB), optionally Ambient Occlusion.
- Export geometry as FBX (`.fbx`). Set scale to **meters** and freeze transforms.

**In Blender:**
- Import the FBX.
- Create a **Principled BSDF** material for each submesh and hook up the baked textures. Use *Non-Color* for Metallic/Roughness/Normal, and a **Normal Map** node into *Normal*.
- (Optional) Pack images: *File → External Data → Pack Resources*.
- Export: *File → Export → glTF 2.0*, choose **Binary (.glb)**. Consider **Draco** compression to reduce size.  
  The exporter handles axis conversions automatically.

**Material Variants (optional):**
- Author variants using the `KHR_materials_variants` extension (via a Blender add-on) and export with that extension.  
  If present, the dropdown on the demo page will list them automatically.

## Local testing
Use a local web server (browsers block file URLs):
- Python: `python -m http.server`
- VS Code: Live Server extension

Then open `http://localhost:8000` and test before pushing.

## Notes
- Keep your GLB under ~50–80 MB for faster loads. Prefer 2–4K textures, KTX2/Basis, and Draco/meshopt.
- Add an empty `.nojekyll` file to bypass Jekyll on Pages (already included).
