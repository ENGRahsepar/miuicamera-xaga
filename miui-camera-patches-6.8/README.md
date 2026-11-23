# MiuiCamera 6.8 xaga patches

Base APK: `Xaga-Leica-6.8.002090.2v2.apk`
(version `6.8.002090.2-kry`, SHA-256
`c3519dfbb1b60a8a679cc385858ee52a5a46506fd4f9ae27d6ec8df51ee349c4`).
Native libraries were pulled from xaga HyperOS 4 `OS4.0.3.0.XPSCNXM`.

Current validated package: `MiuiCamera-6.8.002090.2-4k60-capture-v49.apk`
(SHA-256 `c06beeb13c794e2cc5e1d8c6bdb9313962116715765f7711adc01988c8949e1c`).

Validated fixes included in the prebuilt APK:

- Preserve the static 4K60 unlock, real Portrait bokeh, Documents, and genuine 64 MP output.
- Retry the default JPEG stream map only when the active operating-mode map has no sizes, fixing camera startup on auxiliary lenses.
- Bypass the ultrawide LDC `S_DUAL_Plugin` stall, restoring 0.6x preview and capture in still modes while keeping normal Video working.
- Supply the existing basic Beauty item set when scene 1 has no usable JSON profile; Beauty controls reach the real SkinBeautifier pipeline.
- Use 2048-pixel tiles for large-image rotation, reducing the measured 64 MP save time from 28.4 seconds to 6.7 seconds without allocating two full-size bitmaps.

`0001-Unlock-4K-60-FPS.patch` is the static equivalent of HyperCeiler's
`Unlock4k60` hook. In this exact APK, its DexKit query resolves to
`Lr2/g0;->J(IILl9/g;)Z`; the method returns `true` unconditionally.

Source: <https://github.com/ReChronoRain/HyperCeiler/blob/main/library/libhook/src/main/java/com/sevtinge/hyperceiler/libhook/rules/camera/Unlock4k60.kt>

Additional patch under validation:

- `0002-Preserve-MediaTek-zoom-crop.patch` derives a centered crop from the capture result/request zoom ratio, preferring Xiaomi's `xiaomi.superResolution.cropRegionMtk` request/result tags when MediaTek reports a standard ratio of 1.0 and resets the standard crop to the full sensor. It scales the cropped NV21 data back to the original output size before JPEG compression and logs the selected metadata for validation. Full-size 1.0x captures are returned unchanged, and processing failures preserve the original frame. For the single-DEX test package, the modified `Mp/l$e` processor is staged in `classes3`, which Android loads before the untouched original in `classes10`; no other DEX or payload entry is rebuilt.
