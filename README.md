# PICO Unity SDK Skills

[English](#english) | [中文](#中文)

---

## English

This repository hosts **PICO Unity SDK Skill** documents designed for AI Coding Agents (e.g. Claude Code, Cursor, TRAE), managed per SDK version.

Each SDK version lives on its own branch. The content of each branch can be loaded directly by an Agent as a Skill, helping answer questions about development, configuration, debugging and troubleshooting for that specific SDK version.

### Repository Layout

- `main` branch: repository entry point. Contains only this README and the version index — no Skill content.
- `<version>` branches (e.g. `3.4.0`, `0.11.0`): hold the Skill content for the corresponding SDK version.

### Version Index

| SDK Version | Branch | Status |
| --- | --- | --- |
| 3.4.0 | [`3.4.0`](../../tree/3.4.0) | Released |

### Usage

1. Check out the branch matching your PICO Unity SDK version:

   ```bash
   git clone git@github.com:Pico-Developer/PICO-Unity-SDK-Skills.git
   cd PICO-Unity-SDK-Skills
   git checkout 3.4.0
   ```

2. Load the `pico-unity-sdk/` directory into your AI Coding Agent's Skill path.

### License

Content in this repository follows the relevant terms of the PICO Developer documentation. See each version branch for details.

---

## 中文

本仓库用于存放面向 AI Coding Agent（如 Claude Code / Cursor / TRAE 等）的 **PICO Unity SDK Skill** 文档，按 SDK 版本进行管理。

每个 SDK 版本对应一个独立分支，分支内容可被 Agent 作为 Skill 直接加载，用于回答与该版本 SDK 相关的开发、配置、调试与排错问题。

### 仓库结构

- `main` 分支：仓库入口，仅包含本 README 和版本索引，不存放具体 Skill 内容。
- `<version>` 分支（如 `3.4.0`、`0.11.0`）：对应版本的 Skill 内容。

### 版本索引

| SDK 版本 | 分支 | 状态 |
| --- | --- | --- |
| 3.4.0 | [`3.4.0`](../../tree/3.4.0) | 已发布 |

### 使用方式

1. 根据你正在使用的 PICO Unity SDK 版本，切换到对应分支：

   ```bash
   git clone git@github.com:Pico-Developer/PICO-Unity-SDK-Skills.git
   cd PICO-Unity-SDK-Skills
   git checkout 3.4.0
   ```

2. 将 `pico-unity-sdk/` 目录加载到你的 AI Coding Agent 的 Skill 路径中即可。

### 许可证

本仓库内容遵循 PICO 开发者文档相关条款，详见各版本分支内说明。
