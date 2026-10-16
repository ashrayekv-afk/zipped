# NKPI bilateral calculator — 9.0.6

The new anatomical viewer places the report-derived cornea within a complete reference eyeball. It opens in a natural whole-eye view, with rotation, close-up, curvature/thickness overlays and a tissue cutaway. The existing calculator, regional change maps and cone evolution tracker are retained.

## Install / update

Use the small **NKPI_v906_GitHub_Upload.zip** distribution. It contains four top-level files and one configuration file:

- `kcn_dual_calculator_app.py` — launcher; keep this exact filename as the Streamlit main file.
- `nkpi_runtime.zip` — complete app source, trained-model JSON files, viewer, importer, OCR assets, and retained tests/documentation. Upload this inner ZIP intact.
- `requirements.txt` — tested Python dependencies.
- `README.md` — installation steps.
- `.streamlit/config.toml` — original theme and app settings; keep its folder.

1. Download **NKPI_v906_GitHub_Upload.zip** and use Windows **Extract All** once.
2. Upload the extracted items to the **top level** of the same GitHub repository, replacing the matching launcher and requirements. Upload `nkpi_runtime.zip` as a file; do not extract that inner ZIP for deployment.
3. Keep **kcn_dual_calculator_app.py** as the Streamlit entry point, using the updated repository and branch. Python **3.12** is the tested runtime.
4. Reboot the app, refresh the browser, and confirm **9.0.6-anatomical-eye** in the footer.
5. Re-upload and process the original Pentacam ZIPs after updating, then calculate as usual.
6. Open **Regional change & 3D corneal view → Current case → OD/OS → 3D corneal view**. The **Cone evolution tracker** uses two visits.

The launcher verifies and unpacks the runtime automatically on the server. All Python modules, models, component files, and OCR assets travel together, so `nkpi/` no longer needs a separate GitHub folder upload. Existing older source folders can stay in the repository; the launcher selects this bundled version. No new API key is needed. The existing browser OCR/PDF libraries still need their normal network access.

Local launch: `python -m pip install -r requirements.txt`, then `python -m streamlit run kcn_dual_calculator_app.py`. For source inspection, extract a separate copy of `nkpi_runtime.zip`; it contains the complete ordinary source tree.

## Packaging repair in 9.0.6

This release carries forward all 9.0.5 application features. It changes delivery and cache identifiers, retains the existing dependency declarations, and corrects the old update instructions. The NKPI model artifacts, scoring code, scalar extraction, spatial calculations and 3D rendering implementation are retained.

## Retained latest additions (9.0.5)

- **Whole eye by default:** a continuous corneal shell, reference sclera and iris. Drag or use the camera buttons to rotate. Front, side, zoom and close-up controls remain available.
- **Patient-linked central shape:** standard anterior elevation plus the printed BFS define the report-image estimate; pachymetry determines its inferred inner offset. Native anterior/posterior coordinates remain supported.
- **Smooth gap reconstruction:** unreadable interior areas are continued from neighboring surface data. A smooth peripheral transition connects the central region to the reference eyeball. The default has no missing-data wedges or striped hole patches.
- **Combined view:** curvature color and supported thickness contours share the same 3D surface. Interior missing map colors are interpolated and slightly muted for continuity. These visual fills do not produce measured values.
- **Optional reconstruction view:** source-supported geometry, reconstructed gaps and reference anatomy have separate colors. Source-supported includes the existing image smoothing; it is not synonymous with raw device data.
- **Tissue cutaway:** shows the front/back shell separation. The default keeps equal physical axes. The existing optional elevation emphasis is explicitly labeled.
- **Responsive rendering:** smaller screens use readable labels; dragging uses a lighter display mesh and returns to full detail when released.

## What the uploaded reports support

The automatic image route uses the standard anterior elevation, printed anterior BFS and thickness map from a supported Belin–Ambrósio report. The floating reference's translation and tilt are unavailable, so the result is approximate. Its inner surface is inferred from pachymetry, not independently measured posterior geometry. When elevation cannot be reconstructed, a clearly labeled reference cornea remains available; no patient cone is fabricated from Kmax, NKPI or color alone.

Gap completion changes presentation only. Original missing values, source coverage, NKPI, biological domains, regional measurements and cone tracking remain unchanged. Gap-filled geometry and color do not receive numerical patient readouts. The globe, iris and peripheral transition are illustrative. This is not an exact 1:1 replica or a surgical planning model.

For a closer reconstruction, the existing numerical import accepts anterior/posterior x/y/z grids and device pachymetry with units, laterality and a shared coordinate system. Native heights are retained at supported source nodes; interpolated display geometry remains separate.

Keep complete original report ZIPs. Supported automatic layouts are the original 1200-pixel-wide exports and proportional scaling, with complete titles and legends. Phone photographs, mirrored/rotated pages, cropped legends and undocumented layouts are not automatically calibrated. Regional comparison still uses Topometric/KC-Staging anterior/posterior axial curvature and Belin–Ambrósio thickness. Posterior elevation is not substituted for posterior curvature.

See **docs/SURFACE_DATA.md** for reconstruction details and **docs/TEST_REPORT.md** for verification and limits. Patient scans and private QA files are not included in this package.
