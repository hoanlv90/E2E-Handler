# E2E-Handler User Manual

**Version beta** • **Author: Viet-Hoan Le** • **Email: hoanlv@uw.edu**

E2E-Handler creates en face projection images and retinal thickness maps from Heidelberg SPECTRALIS OCT volume scans. It uses an **AVI file for the OCT images** and the **corresponding E2E file for the segmentation layers and scan information**. Both files are required.

**Workflow:** prepare and correct segmentation in HEYEX → export AVI and E2E → place and name the files → load the volume → generate and review results.

## 1. Prepare your scan in HEYEX

Complete these steps **before opening the data in E2E-Handler**. Menu wording and available export options vary with the HEYEX version and local configuration; use the instructions supplied with your HEYEX installation when a menu differs.

### 1.1 Generate and correct the segmentation

1. Open the required patient, examination and OCT volume in **Heidelberg Eye Explorer (HEYEX)**.
2. Confirm the correct eye, examination date and volume. Use a **regular, parallel raster volume scan**. Radial/star, circular and irregular scan patterns are not supported.
3. Use the HEYEX segmentation function to generate the retinal layer boundaries needed for your analysis.
4. Review the segmentation throughout the volume, scrolling through **all B-scans**. Correct misplaced boundaries, discontinuities, missing segments and sudden layer jumps using the HEYEX editing tools.
5. Save the corrected analysis in HEYEX before exporting.

The default analyses use the layer labels **ILM, INL, PR1, RPE and BM**. In E2E-Handler, **INL denotes the INL–OPL boundary**. A custom slab or thickness map needs both of its selected boundaries to be available. Missing required layers prevent the affected output from being generated.

### 1.2 Export the volume as an AVI file

1. Select the corrected **volume scan thumbnail** in HEYEX.
2. Right-click and choose **Export → as Picture** (also referred to as **Export as pictures**). In versions that provide it, this command is also available from the analysis window's **Image** menu.
3. In the save dialog, choose **AVI (.avi)** as the file type for the volume.
4. Export the **complete B-scan sequence**, with **one AVI frame per B-scan**, in the original scan order. Choose the OCT image's **1:1 Pixel** setting where available and preserve its native pixel dimensions.
5. Disable options that add patient information, labels or graphics, such as **Add Info Block**, **Add Patient Name** and **Add Overlays**. Export the OCT image without segmentation lines or measurement graphics burned into the pixels.
6. Save the AVI using the naming format in [Section 2](#2-place-and-name-the-files).

The AVI may contain a fundus image on the left and an OCT B-scan on the right. This layout is supported: E2E-Handler automatically extracts the **right-hand OCT region**, using the E2E A-line count and depth-pixel count. Keep the OCT panel at its native size and at the top of the frame. If HEYEX offers an option to reduce the fundus panel to the OCT panel's height, it may be used without resizing the OCT panel. Export a B-scan sequence rather than a screen recording, a single B-scan or a rotating 3D view.

The manufacturer describes picture export and its image layout in the [SPECTRALIS Quick Guide, “HEYEX – Image and Data Export”](https://research.unityhealth.to/wp-content/uploads/2015/09/Spectralis-Quick-Guide.pdf). Consult your installed SPECTRALIS manual for version-specific AVI export options.

### 1.3 Export the corresponding E2E file

1. Export the **same volume or examination** as an **E2E (.e2e)** file **after saving the corrected segmentation**. The E2E is needed to retain the segmentation data.
2. In HEYEX versions with a thumbnail context menu, use **Export → as E2E** and choose the destination folder.
3. In HEYEX 2 installations using export templates, open **Export**, select the **E2E** template category, add the required examination/series to the appropriate export template, and export to the destination drive/folder. Wait for successful completion. This workflow is documented in the manufacturer's [HEYEX 2 Basic Navigation and Functions tutorial, Export tab](https://www.academy.heidelbergengineering.com/hedata/e-learning/Totara/Dateien/pdf-tutorials/D4002455-001_HEYEX2_PDFTutorial_BasicNavigationAndFunctions_EN.pdf).
4. Place the exported E2E beside its AVI.

**If you correct the segmentation later, save it in HEYEX and export the E2E again before repeating the analysis.** If you change the selected volume or its image geometry, export both files again. An older E2E will not contain your latest segmentation corrections.

## 2. Place and name the files

For automatic loading, place the matching AVI and E2E **in the same folder** and use these names:

| File | Recommended filename | Example |
| --- | --- | --- |
| OCT volume AVI | `subjectID_eye_YYYYMMDD.avi` | `TEST000_OS_20220224.avi` |
| Corresponding E2E | `subjectID.e2e` | `TEST000.e2e` |

- Use the **same subject ID** in both filenames. A study ID can be used.
- Use **OD** for the right eye or **OS** for the left eye.
- Use the actual scan date: **YYYYMMDD** means four-digit year, two-digit month and two-digit day. For example, `20220224` means **24 February 2022**.
- Ensure the filename eye and date agree with the corresponding E2E series.
- Uppercase or lowercase file extensions are accepted. An E2E visit suffix such as `TEST000_V0.E2E` is also supported.

Example folder, using illustrative filenames:

```text
OCT_data/
└── TEST000_OS_20220224/
    ├── TEST000_OS_20220224.avi
    └── TEST000.e2e
```

Use separate folders for different volumes when the subject, eye and date are identical. Keep a single intended E2E beside each AVI to avoid ambiguous matches. One E2E can contain multiple volumes; you may still need to select the correct series when loading.

Files with other names can be paired using **Match E2E…**, as described below. Renaming or manually pairing files does not anonymize their contents.

## 3. Start the application and load data

1. Download the Windows application package from the GitHub repository's **Releases** page and extract the entire package to a folder you can write to. Keep the supplied files and subfolders together.
2. Double-click **E2E-Handler.exe**.
   If Windows reports a missing Visual C++ runtime DLL, run the included **Prerequisites/VC_redist.x64.exe** installer, then start E2E-Handler again.
3. Open **1 • Load data** and click **Browse…** to select the data folder. Enable **Include subfolders** if needed, then click **Scan folder**. Use **Single AVI…** to select one AVI instead.
4. Review the AVI table:

   | Status | Meaning / action |
   | --- | --- |
   | **Auto matched** | A corresponding E2E filename was found. Confirm the volume after loading. |
   | **Manual match** | A user-confirmed pairing is available. |
   | **Unmatched** with a warning flag | Select the row to read the reason, then correct the filename/location or use **Match E2E…**. |

5. Check **Use** for the desired matched files and click **Load selected →**. Unresolved files cannot be selected for loading.
6. Review each loaded volume's dimensions and physical spacing. Dimensions are shown as **B-scans × depth pixels × A-lines**.
7. Select a loaded volume and click **Match / spacing / crop…** when you need to choose a different E2E series or review the match. Confirm the eye, date, B-scan count, image orientation and OCT crop. Check the fast-axis, axial and B-scan spacing against the original HEYEX scan information. These values determine the physical scale and thickness measurements.

The crop is automatic. An AVI smaller than the selected E2E OCT dimensions cannot be loaded as that volume. Only change **reverse frame order** or **horizontal flip** when the preview and HEYEX data show that the exported sequence requires it.

### Pairing an unmatched AVI manually

1. Select the AVI row and click **Match E2E…**, or double-click the row.
2. Choose the E2E exported from the same scan.
3. Select the corresponding series and confirm the **subject ID**, **eye** and **imaging date**. Confirmed values are used in the exported results and DICOM metadata.
4. Review the dimensions, spacing, orientation and automatic OCT crop. The AVI frame count must equal the E2E series' B-scan count.
5. Click **Match files**, check **Use**, then click **Load selected →**.

Manual matches and their confirmed settings are remembered on this computer. If files are moved, match them again as needed. The source files are not renamed.

## 4. Generate en face projections

1. Open **2 • Projections** and check the volumes to process.
2. Select a slab row to edit its **Name**, **Start layer**, start **Offset (µm)**, **End layer**, end **Offset (µm)** and **Method**. Use **Add slab** for additional outputs or **Remove selected** to delete a slab.
3. Positive offsets move **deeper** into the image relative to the selected boundary. The starting boundary is included and the ending boundary is excluded.
4. Choose the projection method: **mean**, **max**, **min**, **sum**, **mean of 5 max pixels** or **mean of 5 min pixels**.
5. Choose an output location with **Output folder…**, or leave the default **beside each AVI**. **Use AVI folders** restores the default location.
6. Click **Generate projection images** and wait for completion. Use **Open last output** to open the result folder.

The initial slabs are:

| Slab | Start | End | Method |
| --- | --- | --- | --- |
| Slab 1 | ILM + 0 µm | RPE + 0 µm | Mean |
| SubRPE slab | BM + 64 µm | BM + 400 µm | Mean |

**SubRPE slab** stops at the available image depth at each A-line. For example, where the image extends only 350 µm below BM, the slab uses **64–350 µm below BM**. A slab entirely outside the available image cannot produce a result; other valid outputs can still complete.

## 5. Generate thickness maps

1. Open **3 • Thickness maps** and check the volumes to process.
2. Review the default map definitions:

   | Map | Start layer | End layer |
   | --- | --- | --- |
   | Full retina thickness | ILM | RPE |
   | RPE elevation | RPE | BM |
   | Outer retinal thickness | INL | RPE |
   | Photoreceptor thickness | PR1 | RPE |

3. Edit names, boundaries and display settings as needed. The first four map rows can be edited but cannot be removed. Use **Add map** to create additional definitions.
4. Set **Sigma (px)** to control map smoothing; **0** disables it. Sigma is measured in output-map pixels. Choose a **Colormap** and the **Min (µm)** / **Max (µm)** display range. These display limits do not clip the raw thickness values.
5. Confirm the output location and click **Generate thickness maps**.
6. Open the output folder and review the maps, including the versions with a colorbar.

You can generate projections and thickness maps from the same loaded volumes without loading them again.

## 6. Review B-scans and segmentation

The preview initially displays a saved **TEST000 reference B-scan**. This is an example, not a preview of a newly loaded volume.

After a volume has been processed, select it in the processing tab to review its actual B-scans and segmentation. Use the **B-scan slider**, number control or **Prev** / **Next** buttons to inspect the whole volume. Select a slab or map row to review its boundaries, shown as two thicker dotted white lines. The image and layer lines fit the preview width; scroll vertically if the image is taller than the panel.

Review the layer positions across all B-scans before interpreting the generated images. If a layer needs correction, return to HEYEX, correct and save it, then re-export the E2E. In **1 • Load data**, remove the affected loaded volume with **Remove selected**, scan/load the updated pair again, and regenerate the results.

### Optional layer smoothing

Enable **Apply 2D median filter to layers** in **Layer smoothing** when appropriate. The initial window sizes are **3 B-scans × 5 A-scans**. Use odd sizes; **1** disables filtering along that axis. This setting applies to both projection and thickness generation. Larger windows may also smooth real anatomical features, so inspect the resulting layers.

Layer smoothing does not replace segmentation review in HEYEX. A processed volume's preview reflects its completed run; after changing smoothing settings, generate the results again to review the change.

## 7. Find and use the output files

Each run creates a new folder, so earlier results remain available:

```text
<AVI filename without .avi>/
├── Proj_run_<date_time>/
└── Thickness_run_<date_time>/
```

By default, the AVI-named folder is created beside the AVI. A custom **Output folder…** places results under that location instead. Folder timestamps distinguish separate runs.

| Output | Format and purpose |
| --- | --- |
| `prj_01_<slab_name>.tiff` | **8-bit grayscale** projection image for viewing/export. |
| `prj_01_<slab_name>.dcm` | **16-bit** derived projection image in DICOM format. |
| `T_01_<map_name>_raw_um.tiff` | **32-bit floating-point** thickness values in **µm**, for quantitative analysis. |
| `T_01_<map_name>_color.tiff` | Color thickness map using the selected display range. |
| `T_01_<map_name>_colorbar.tiff` | Color thickness map with a **µm colorbar on the right**. |
| `report.json` | Run summary, including any outputs that could not be generated. |

The number indicates the slab/map order. Use the **raw µm TIFF** for thickness measurements; the colored images are for display. Projection TIFF and DICOM files use different intensity encodings, so their stored pixel values should not be compared directly.

Check the completion message. A **partial** run may contain valid completed images while other requested outputs are missing. **Cancel** may leave completed files in the run folder; review the run summary before using them.

## 8. Settings and troubleshooting

Use **Save configuration** / **Load configuration** to reuse analysis definitions and layer-smoothing settings. Choose **classic** or **dark** from the **Theme** menu; the theme is remembered on this computer.

| Problem | What to check |
| --- | --- |
| AVI is flagged as unmatched | Confirm the same subject ID, OD/OS, scan date and folder, or use **Match E2E…**. |
| Several possible E2E files or series | Keep the intended E2E beside the AVI and select the series matching the eye, date and B-scan count. |
| B-scan counts or OCT dimensions differ | Confirm both exports came from the same complete volume. Re-export at native pixel size with one frame per B-scan. |
| Preview shows only the TEST000 example | Process the intended volume, then select it in the processing tab. |
| Layers do not follow the OCT image | Check the selected E2E series, frame order and orientation. Review/correct segmentation in HEYEX and re-export the E2E. |
| A slab or map is missing | Read the completion message/run summary. Check that its boundaries exist and that the slab lies within the image depth. |
| Thickness scale seems incorrect | Verify the physical spacing against HEYEX and confirm the intended layer pair. |
| Application does not open | Extract the full release package again and keep its supplied files together. Record the startup error and include the indicated startup log when reporting the issue. |

For support, use the repository's **Issues** page and include the release version, steps to reproduce and the exact error message. Remove patient information from screenshots, logs and example files before sharing. E2E-Handler does not anonymize the input AVI or E2E files.
