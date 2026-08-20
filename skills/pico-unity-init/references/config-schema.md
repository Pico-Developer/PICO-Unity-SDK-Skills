# .pico-cli/config.json 结构

初始化完成后写入 `$PROJECT_ROOT/.pico-cli/config.json`。

## 字段

| 字段            | 来源步骤 | 类型           | 取值                                                                                                      |
| --------------- | -------- | -------------- | --------------------------------------------------------------------------------------------------------- |
| `project_name`  | 自动     | string         | 当前项目所在目录的目录名(`$PROJECT_ROOT` 的 basename)                                                     |
| `sdk`           | 步骤 1   | string(单选)   | `openxr` \| `picoxr`                                                                                      |
| `unity_version` | 步骤 2   | string         | 选定的 Unity 6+ LTS 完整版本号,如 `6000.0.73f1`                                                           |
| `platform`      | 固定     | string         | 固定为 `android`(PICO 为 Android 平台,不可选其它平台)                                                     |
| `devices`       | 步骤 6   | string[](多选) | `pico swan`、`pico 4 ultra`                                                                               |
| `business_type` | 步骤 7   | string(单选)   | `toB` \| `toC`。表单问「是否开发企业版?」,选「是」→ 存 `toB`,选「否」→ 存 `toC`(存最终值,不存「是 / 否」) |

## 示例

```json
{
  "project_name": "MyPicoApp",
  "sdk": "picoxr",
  "unity_version": "6000.0.73f1",
  "platform": "android",
  "devices": ["pico swan", "pico 4 ultra"],
  "business_type": "toB"
}
```

> 若 `.pico-cli/` 目录不存在,先创建目录再写入文件。config.json 的存在即代表项目已完成初始化,后续再次触发 skill 时应据此判断跳过初始化。
