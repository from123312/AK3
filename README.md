<div align="center">

# GKI KernelSU SUSFS

### Xiaomi Kernels · KernelSU / KernelSU-Next / SukiSU / ReSukiSU + SUSFS

[![KernelSU](https://img.shields.io/badge/KernelSU-Supported-5AA300?style=flat-square)](https://kernelsu.org/)
[![KernelSU Next](https://img.shields.io/badge/KernelSU--Next-Supported-5AA300?style=flat-square)](https://kernelsu-next.github.io/webpage/)
[![SukiSU](https://img.shields.io/badge/SukiSU-Supported-5AA300?style=flat-square)](https://sukisu.org/)
[![ReSukiSU](https://img.shields.io/badge/ReSukiSU-Supported-5AA300?style=flat-square)](https://resukisu.github.io/)
[![SUSFS](https://img.shields.io/badge/SUSFS-Integrated-E67E22?style=flat-square)](https://gitlab.com/simonpunk/susfs4ksu)
[![GitHub Actions](https://img.shields.io/badge/Build-GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)](../../actions)

</div>

## 📖 简介

本仓库基于 [AnyKernel3](https://github.com/osm0sis/AnyKernel3) 构建，通过 GitHub Actions 自动编译 **Android GKI 内核**，集成多种 KernelSU 变体与 SUSFS 文件系统隐藏方案，并附加 ZRAM、防格机等实用补丁。

- 构建工作流修改自 [zzh20188/GKI_KernelSU_SUSFS](https://github.com/zzh20188/GKI_KernelSU_SUSFS) 与 [Wild Kernels](https://github.com/WildKernels/GKI_KernelSU_SUSFS)
- 刷入规则：***只要内核版本匹配即可刷入***

## 📦 支持的内核版本

| Android | 内核版本 | 手动触发工作流 |
|:---:|:---:|:---:|
| 12 | 5.10 | `kernel-a12-5-10.yml` |
| 13 | 5.15 | `kernel-a13-5-15.yml` |
| 14 | 6.1 | `kernel-a14-6-1.yml` |
| 15 | 6.6 | `kernel-a15-6-6.yml` |
| 16 | 6.12 | `kernel-a16-6-12.yml` |
| 自定义 | 任意 | `kernel-custom.yml` |

## ✨ 功能特性

| 特性 | 说明 |
|:---|:---|
| 🔐 KernelSU 全家桶 | 支持 Official / Next / SukiSU / ReSukiSU 四种变体，构建时按需选择 |
| 🙈 SUSFS | 文件系统级隐藏，配合 KSU 完成环境伪装 |
| 💾 ZRAM LZ4 | ZRAM 压缩算法增强补丁栈 |
| 🛡️ BBG 防格机 | 添加 BBG 防格机补丁，降低分区损坏风险 |
| ⚡ KPM | 可选开启 KPM 功能 / 构建期修补 |
| 🔔 Re-Kernel | 可选集成 Re-Kernel 驱动 |
| 🩹 CVE-2026-43499 | 可选自动应用 rtmutex 修复补丁 |
| 📱 一加 8E 支持 | 可选添加一加 8E 处理器支持 |
| 🐳 Droidspaces | 可选容器支持及 NTSync 内核兼容补丁 |
| 🐦 HMBird Patch | 强制 OPLUS HMBird 内核类型 `HMBIRD_OGKI → HMBIRD_GKI`，让自编内核绕过限制 |

## 🚀 使用方法

1. **Fork 本仓库**（或直接使用本仓库）
2. 进入 **Actions** 页面，选择对应内核版本的工作流
3. 点击 **Run workflow**，按需填写参数：
   - `android_version` / `kernel_version` / `sub_level` / `os_patch_level`（内核版本四件套）
   - `ksu_variant`：KernelSU 变体（Official / Next / SukiSU / ReSukiSU）
   - 功能开关：`enable_susfs`、`use_zram`、`use_bbg`、`use_kpm` 等
4. 构建完成后，在本次运行页面下载 **Artifacts**：
   - `AnyKernel3.zip` —— 卡刷包（推荐，配合自定义 Recovery 或 KSU 刷入）
   - `boot.img` / `boot-gz.img` / `boot-lz4.img` —— 对应压缩格式的 boot 镜像

> 💡 产物默认上传为 Actions Artifacts，不自动发布 Release；失败时会额外上传构建日志（`Build-Logs`）与补丁冲突记录（`Rejects`）供排查。

## 📂 仓库结构

```
.
├── .github/workflows/   # 构建工作流（分版本 + 通用 + 自动触发）
├── config/              # 内核配置
├── data/                # 内核版本 JSON 数据（含 Android 16）
├── scripts/             # 辅助脚本
├── security_patch/      # 安全补丁
├── zram/                # ZRAM LZ4 补丁
├── hmbird_patch.c       # HMBird 内核类型修补
└── .gitattributes       # 补丁文件换行管理
```

## 🙏 致谢

- [osm0sis/AnyKernel3](https://github.com/osm0sis/AnyKernel3) — 万能刷入模板
- [zzh20188/GKI_KernelSU_SUSFS](https://github.com/zzh20188/GKI_KernelSU_SUSFS) / [WildKernels/GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS) — 构建工作流基础
- [KernelSU](https://kernelsu.org/) / [KernelSU-Next](https://kernelsu-next.github.io/webpage/) / [SukiSU](https://sukisu.org/) / [ReSukiSU](https://resukisu.github.io/)
- [SUSFS](https://gitlab.com/simonpunk/susfs4ksu)

<div align="center">

## ⚠️ 免责声明

刷入内核不会使设备失去保修，但刷机始终存在变砖风险，请务必：

- 💾 **提前备份系统原始 boot 镜像**
- 🧠 **充分了解刷机风险后再操作**
- 若刷入 AnyKernel3 后设备无限重启或无法开机，请进入 BootLoader 刷回原始 boot 镜像
- 因刷入本内核造成的任何问题，本人概不负责

# **🚨 后果自负，风险自担！**

</div>
