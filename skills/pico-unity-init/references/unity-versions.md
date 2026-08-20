# Unity 版本判断与 LTS 清单

## 判断当前项目 Unity 版本

读取 `$PROJECT_ROOT/ProjectSettings/ProjectVersion.txt`,示例内容:

```
m_EditorVersion: 6000.0.73f1
m_EditorVersionWithRevision: 6000.0.73f1 (a166abc3bf0e)
```

`m_EditorVersion` 的第一段即主版本号:

- `6000.x.y` → Unity 6(即 "Unity 6 及以后")。
- 主版本号 `< 6000`(如 `2022.3.x`、`2021.3.x`)→ 低于 Unity 6。

## "Unity 6 之后的 LTS" 候选清单

在向开发者展示可选版本时,列出 Unity 6 系列的 LTS 版本。以官方最新 LTS 发布为准,展示前建议实时确认最新补丁号。当前可选(示例):

- `6000.0.x` LTS（Unity 6.0 LTS）— 例如 `6000.0.73f1`
- `6000.1.x` LTS（后续 LTS，如已发布）
- `6000.2.x` LTS（后续 LTS，如已发布）

> 说明:仅列出 Unity 6(6000 系列)及以后的 LTS 版本。具体可用的补丁版本请以 Unity 官方 LTS 发布页为准。展示时建议给出完整版本号(含 `f1` 之类的后缀),以便 Unity CLI 精确定位安装。

## 查询本机已安装的 Unity 编辑器

用 **Unity CLI**(而非 Unity Hub)列出本机已安装的编辑器(由本地 agent 直接在开发者本机的本地 shell 中执行):

```
unity editors --installed
```

> 说明:本 skill 统一使用 Unity CLI(与「注册并打开项目」阶段保持一致的工具链),不使用 Unity Hub。输出为已安装版本号列表(如 `6000.0.73f1`)。据此把候选 LTS 拆成两组。

## 版本选择的两组清单(对应阶段 C 表单的版本选项)

向开发者展示时**必须分成两类**:

- **2.1.1 已安装列表**:上面 `unity editors --installed` 查到的、且属于 Unity 6+ LTS 的版本。开发者选中其一 → 直接作为 `unity_version`,无需安装。
- **2.1.2 未安装列表**:官方 Unity 6+ LTS 中本机尚未安装的版本。开发者若选中其一 → 先用下面命令安装该版本,再作为 `unity_version`。

安装新 Unity 版本(**必须用 `-m android` 捆绑安装 Android Build Support**,PICO 为 Android 平台):

```
unity install <VERSION> -m android
```

若某个已安装版本缺少 Android 模块,用以下命令为该已有版本补装 Android(查看输出中的 **Status** 列判断该模块是否已安装):

```
unity install-modules -e <VERSION> -m android
```

> 若本机未安装 Unity CLI,提示开发者先安装 Unity CLI 后再继续。安装大版本耗时较长,执行前告知开发者。

### 安装后同步到 Unity Hub

通过 `unity install` 安装的编辑器,可能不会自动出现在 Unity Hub 的「已安装编辑器」列表里(Unity Hub 无记录)。安装完成后,把该编辑器路径注册进 Unity Hub,使其可见:

- 定位安装路径:`unity editors --installed` 输出中该版本对应的 editor 可执行文件/安装目录。
- 让 Unity Hub 收录该路径(任选其一):
  - Unity Hub 图形界面:Installs → 右上角 `Locate`(定位已有安装)→ 选中该版本的安装目录;
  - 或通过 Unity Hub CLI 添加已安装编辑器路径(`... --headless install-path --set` / `editors --add <PATH>`,以本机 Hub 版本支持的子命令为准)。

> 说明:版本的查询与安装统一走 **Unity CLI**;仅在「让 Hub 也能看到该编辑器」这一步涉及 Unity Hub 的收录操作。若开发者不使用 Unity Hub,可跳过本小节。

## 注册并打开项目(对应阶段 D.7)

初始化收尾时,先把项目注册进 Unity 的已知项目列表(便于开发者日后从项目列表直接找到并打开),再用选定版本打开,并强制目标平台为 Android:

```
unity projects add /path/to/PROJECT_ROOT
unity open /path/to/PROJECT_ROOT --build-target Android
```

- `unity projects add <PROJECT_ROOT>`:将项目加入 Unity 已知项目列表,不启动编辑器。
- `unity open ... --build-target Android`:以选定的 `unity_version` 打开该项目,并将 Active Build Target 切为 **Android**。PICO 为 Android 平台,禁止 Windows / macOS / WebGL 等其它平台。若本机存在多个版本,确保打开时使用的是表单中选定的版本;若该版本缺少 Android Build Support,请先补装 Android 模块再打开(安装新版本用 `unity install <VERSION> -m android`,已有版本补装用 `unity install-modules -e <VERSION> -m android`,查看输出 **Status** 列确认是否已装)。
