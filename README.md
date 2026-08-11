# PICO Unity SDK Skills

[English](#english) | [中文](#中文)

---

## English

This repository hosts **PICO Unity SDK Skill** documents designed for AI Coding Agents (e.g. Claude Code, Cursor, TRAE), organized by SDK version.

Each SDK version lives on its own branch. The content of each branch can be loaded directly by an Agent as a Skill, helping answer questions about development, configuration, debugging and troubleshooting for that specific SDK version.

### Repository Layout

- `main` branch: repository entry point. Contains only this README and the version index — no SDK Skill content.
- `<version>` branches (e.g. `6.0.0`, `3.4.0`, `0.11.0`): hold the Skill content for the corresponding SDK version.

### Version Index

| SDK | SDK Version | Branch | Status | Scope |
| --- | --- | --- | --- | --- |
| PICO Unity SDK | 6.0.0 | [`6.0.0`](../../tree/6.0.0) | Released | PICO XR / Unity OpenXR / PICO Spatial: project inspection, mode selection, migration, controllers, hands, eye/body tracking, passthrough, anchors, spatial mesh, foveated rendering, compositor layers, haptics, spatial camera/input/UI, Android build configuration, diagnostics and on-device validation. |
| PICO Unity Integration SDK | 3.4.0 | [`3.4.0`](../../tree/3.4.0) | Released | PICO XR mode: project setup, Passthrough, Controller / Hand Tracking, Foveated Rendering, App SpaceWarp, tools and troubleshooting. |
| PICO Unity SDK | 0.11.0 | [`0.11.0`](../../tree/0.11.0) | Released | PICO XR / Unity OpenXR / PICO Spatial: mode selection and migration, input and tracking, MR / Passthrough / Spatial Anchors / Scene / Spatial Mesh, Platform & Enterprise Services, SecureMR, composition layers & MRC, Spatial Audio, performance and build / release troubleshooting. |

### Usage

1. Check out the branch matching your PICO Unity SDK version:

   ```bash
   git clone git@github.com:Pico-Developer/PICO-Unity-SDK-Skills.git
   cd PICO-Unity-SDK-Skills

   # PICO Unity SDK 6.0.0
   git checkout 6.0.0

   # PICO Unity Integration SDK 3.4.0
   git checkout 3.4.0

   # PICO Unity SDK 0.11.0
   git checkout 0.11.0
   ```

2. Load the Skill entry for that branch in your AI Coding Agent (Claude Code / Cursor / TRAE, etc.). Older branches may use a top-level `SKILL.md` plus `references/`; newer branches may use a named Skill directory such as `develop-pico-unity-apps/`.

### License

Content in this repository follows the relevant terms of the PICO Developer documentation. See each version branch for details.

---

## 中文

本仓库用于存放面向 AI Coding Agent（如 Claude Code / Cursor / TRAE 等）的 **PICO Unity SDK Skill** 文档，按 SDK 版本组织。

每个 SDK 版本对应一个独立分支，分支内容可被 Agent 作为 Skill 直接加载，用于回答与该版本 SDK 相关的开发、配置、调试与排错问题。

### 仓库结构

- `main` 分支：仓库入口，仅包含本 README 和版本索引，不存放具体 SDK Skill 内容。
- `<version>` 分支（如 `6.0.0`、`3.4.0`、`0.11.0`）：对应版本的 Skill 内容。

### 版本索引

| SDK | SDK 版本 | 分支 | 状态 | 内容范围 |
| --- | --- | --- | --- | --- |
| PICO Unity SDK | 6.0.0 | [`6.0.0`](../../tree/6.0.0) | 已发布 | 覆盖 PICO XR / Unity OpenXR / PICO Spatial 三种模式：项目检查、模式选型、迁移、手柄、手部追踪、眼动/体感追踪、Passthrough、Anchor、Spatial Mesh、Foveated Rendering、合成层、触觉、Spatial Camera/Input/UI、Android 构建配置、诊断与真机验证。 |
| PICO Unity Integration SDK | 3.4.0 | [`3.4.0`](../../tree/3.4.0) | 已发布 | PICO XR 模式：项目搭建与配置、Passthrough、手柄/手部追踪、Foveated Rendering、App SpaceWarp、调试工具与常见问题排查。 |
| PICO Unity SDK | 0.11.0 | [`0.11.0`](../../tree/0.11.0) | 已发布 | 覆盖 PICO XR / Unity OpenXR / PICO Spatial 三种模式：模式选型与迁移、输入与追踪、MR / Passthrough / Spatial Anchor / Scene / Spatial Mesh、Platform & Enterprise Services、SecureMR、合成层与 MRC、Spatial Audio、性能优化以及构建/发布排错。 |

### 使用方式

1. 根据你正在使用的 PICO Unity SDK 版本，切换到对应分支：

   ```bash
   git clone git@github.com:Pico-Developer/PICO-Unity-SDK-Skills.git
   cd PICO-Unity-SDK-Skills

   # PICO Unity SDK 6.0.0
   git checkout 6.0.0

   # PICO Unity Integration SDK 3.4.0
   git checkout 3.4.0

   # PICO Unity SDK 0.11.0
   git checkout 0.11.0
   ```

2. 将该分支的 Skill 入口加载到你的 AI Coding Agent（Claude Code / Cursor / TRAE 等）。旧版本分支可能使用顶层 `SKILL.md` 和 `references/` 目录；新版本分支可能使用命名 Skill 目录，例如 `develop-pico-unity-apps/`。

### 许可证

本仓库内容遵循 PICO 开发者文档相关条款，详见各版本分支内说明。
