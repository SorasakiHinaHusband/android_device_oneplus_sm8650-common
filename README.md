# OnePlus sm8650 (pineapple) common device tree

Common device tree for OnePlus devices based on the Qualcomm SM8650 platform.
Used by the OnePlus 12 (`waffle`) MikuUI build.

## Maintainer

- **SorasakiHinaHusband** — <https://github.com/SorasakiHinaHusband>

## Branch

- `Cinderella` — MikuUI (Android 17 / BP2A)

## Dependencies

| Path | Repository |
| --- | --- |
| `hardware/oplus` | `LineageOS/android_hardware_oplus` |
| `hardware/lineage/interfaces` | provided by the MikuUI manifest |
| `kernel/oneplus/sm8650` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650` |
| `kernel/oneplus/sm8650-devicetrees` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650-devicetrees` |
| `kernel/oneplus/sm8650-modules` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650-modules` |
| `vendor/oneplus/sm8650-common` | `SorasakiHinaHusband/proprietary_vendor_oneplus_sm8650-common` |

## Notes

- `TARGET_NEEDS_DTBOIMAGE := false` together with `BOARD_PREBUILT_DTBOIMAGE`
  makes the build reuse the prebuilt `dtbo.img` from the waffle tree and re-sign
  it with AVB instead of regenerating it from the kernel DTBs.
- Kernel modules are built out-of-tree from `kernel/oneplus/sm8650-modules`
  (`TARGET_KERNEL_EXT_MODULES`).
- The alert slider service is appended to `init/init.target.rc`, which is
  imported by `init.qcom.rc`; standalone rc files in `/vendor/etc/init` are not
  parsed early enough on this platform.
- `TARGET_GRALLOC_HANDLE_HAS_UBWCP_FORMAT := true` is required by the display HAL
  (`gr_ubwcp_utils.cpp`).

## License

Licensed under the Apache License, Version 2.0, unless stated otherwise in the
individual source files. Copyright notices and SPDX tags are retained from the
original authors as required by the license.
