# MiuiCamera 6.8 xaga patches

Base APK: `Xaga-Leica-6.8.002090.2v2.apk`
(version `6.8.002090.2-kry`, SHA-256
`c3519dfbb1b60a8a679cc385858ee52a5a46506fd4f9ae27d6ec8df51ee349c4`).
Native libraries were pulled from xaga HyperOS 4 `OS4.0.3.0.XPSCNXM`.

`0001-Unlock-4K-60-FPS.patch` is the static equivalent of HyperCeiler's
`Unlock4k60` hook. In this exact APK, its DexKit query resolves to
`Lr2/g0;->J(IILl9/g;)Z`; the method returns `true` unconditionally.

Source: <https://github.com/ReChronoRain/HyperCeiler/blob/main/library/libhook/src/main/java/com/sevtinge/hyperceiler/libhook/rules/camera/Unlock4k60.kt>
