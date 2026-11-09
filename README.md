# 一加 SM8650（pineapple）通用设备树 🧩

这是给高通 SM8650 平台的一加机型准备的「公共零件箱」，
一加 12（`waffle`）的 MikuUI 构建就是从这里搬东西的。

## 谁在管这棵树

**SorasakiHinaHusband** —— 有锅我背，有 bug 请提 issue 🙏

## 分支

`Cinderella` —— MikuUI（Android 17 / BP2A）。

## 依赖

| 路径 | 仓库 |
| --- | --- |
| `hardware/oplus` | `LineageOS/android_hardware_oplus` |
| `hardware/lineage/interfaces` | MikuUI manifest 自带 |
| `kernel/oneplus/sm8650` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650` |
| `kernel/oneplus/sm8650-devicetrees` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650-devicetrees` |
| `kernel/oneplus/sm8650-modules` | `SorasakiHinaHusband/android_kernel_oneplus_sm8650-modules` |
| `vendor/oneplus/sm8650-common` | `SorasakiHinaHusband/proprietary_vendor_oneplus_sm8650-common` |

## 那些「不看会踩坑」的设定

- `TARGET_NEEDS_DTBOIMAGE := false` + `BOARD_PREBUILT_DTBOIMAGE`：让构建直接复用
  waffle 树里的 `dtbo.img`，再用 AVB 重新签名，而不是拿内核 DTB 现场重造。
  顺便避免了 out 目录被反复改写导致 soong 疯狂重新分析。
- `TARGET_KERNEL_EXT_MODULES` 里的模块住在 `kernel/oneplus/sm8650-modules`，
  在源码树外编译。
- 三段式拨动键的 service 是**追加**到 `init/init.target.rc` 的（它被 `init.qcom.rc`
  显式 import），别想着丢个独立 rc 到 `/vendor/etc/init` 就能跑。
- `TARGET_GRALLOC_HANDLE_HAS_UBWCP_FORMAT := true`：没有它，display HAL 的
  `gr_ubwcp_utils.cpp` 会当场罢工。

## 许可证

除非文件里另有说明，否则按 Apache License 2.0 授权。
版权声明和 SPDX 标识原样保留，这是底线。
