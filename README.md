# E2E-Handler beta

En face projection images, retinal thickness maps and B-scan segmentation review for Heidelberg SPECTRALIS OCT volumes.

**Author:** Viet-Hoan Le · **Email:** hoanlv@uw.edu

## Download

Download **E2E-Handler-beta-Windows-x64.zip** from the [beta release](https://github.com/hoanlv90/E2E-Handler/releases/tag/beta).
Extract the entire ZIP to a writable folder, then double-click **E2E-Handler.exe**. Keep all supplied files and folders together. Python and HEYEX are not required to run the app; HEYEX is used to prepare your own input data.

The package includes the Windows x64 application, **TEST000 AVI/E2E sample data**, an offline HTML manual, a Markdown manual and a quick-start guide. It is intended for Windows 10/11 (64-bit). This is a beta release; review all segmentation and outputs before using results.

If Windows reports a missing Visual C++ runtime, run the included **Prerequisites/VC_redist.x64.exe** installer and start the app again.

## Try the sample

1. Start **E2E-Handler.exe** and open **1 • Load data**.
2. Browse to the included **SampleData** folder and click **Scan folder**.
3. Load **TEST000_OS_20220224.avi**, automatically paired with **TEST000.e2e**.
4. Open **2 • Projections** or **3 • Thickness maps**, select the volume and generate the images.
5. Use the B-scan preview controls to review the completed volume and its segmentation.

## Prepare your own data

In HEYEX, generate and correct segmentation across the full volume, save it, export the volume as an AVI using **Export → as Picture**, then export its corresponding E2E after the corrections. Put both files in one folder with matching subject IDs. See the [User Manual](USER_MANUAL.md) for export settings, naming and analysis instructions, or open **USER_MANUAL.html** inside the downloaded package for an offline copy.

## Features

- Custom projection slabs, including the default SubRPE mean slab (64–400 µm below BM).
- Thickness maps with raw µm TIFFs, color images and colorbars.
- 8-bit TIFF and 16-bit DICOM projection exports.
- B-scan navigation and segmentation/slab previews.
- Automatic file pairing, manual matching and optional layer smoothing.
- Classic and dark themes.

## Distribution and support

This public repository distributes application binaries and documentation. **Application source code is not published.** GitHub's automatic “Source code” archives contain repository documentation, not a runnable application; download the Windows ZIP instead.

The application's binary-use terms are in [LICENSE.txt](LICENSE.txt). Open-source libraries retain their own licenses; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Corresponding third-party library sources are provided as a separate release download. They do not contain E2E-Handler source code.

Report problems through [Issues](https://github.com/hoanlv90/E2E-Handler/issues), including the beta version, steps and the exact error. Remove patient information before sharing screenshots or files.
