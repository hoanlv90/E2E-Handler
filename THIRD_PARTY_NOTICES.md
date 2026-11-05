# Third-party notices

E2E-Handler beta uses unmodified open-source libraries. Their copyrights and licenses remain in effect independently of the application license.

The Windows package contains full installed license notices in **ThirdPartyLicenses** and a version inventory in **ThirdPartyLicenses/packages.json**. Main libraries include Python (PSF), NumPy/SciPy/scikit-image (BSD), OpenCV (Apache 2.0, plus its third-party notices), FFmpeg (LGPL 2.1 or later), Matplotlib (Matplotlib license), Pillow (HPND), pydicom (MIT), tifffile (BSD), oct-converter (MIT), and Qt/PySide6/Shiboken (LGPL 3).

**PyQt is not included in the release.** Qt 6.8.3, PySide6/Shiboken 6.8.3 and OpenCV's FFmpeg 20240522 decoder are dynamically loaded, replaceable libraries. The corresponding library source archives, original build instructions, licenses and checksums are included in **E2E-Handler-beta-ThirdPartySources.zip**, available beside the application ZIP on the [release page](https://github.com/hoanlv90/E2E-Handler/releases/tag/beta). These are third-party sources, not E2E-Handler source.

To use modified compatible libraries, extract the application folder, replace the matching DLL/PYD files in place and retain the required x64/Python 3.12/Qt ABI compatibility. No signature or integrity lock prevents library replacement. You may debug or reverse engineer the combined program for modifying these LGPL libraries. The third-party archive includes further build information.

The executable was compiled with **Nuitka 4.3.4**. Its runtime is covered by AGPLv3 with the [Nuitka Runtime Library Exception](https://github.com/Nuitka/Nuitka/blob/develop/LICENSE-RUNTIME.txt), which explicitly permits proprietary compiled applications. Its notices, exception text and unmodified corresponding runtime/compiler sources are included in the third-party materials. E2E-Handler source is not included.

See the [Qt licensing obligations](https://www.qt.io/development/open-source-lgpl-obligations) and [FFmpeg legal information](https://ffmpeg.org/legal.html) for their terms. The bundled license texts govern.
