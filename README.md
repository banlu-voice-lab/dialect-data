# 桂林方言 TTS 训练数据集 · 人工标注工作区

## 一、标注工具：segment_editor.html

本目录自带 `segment_editor.html`，是一个**纯浏览器**的单文件标注编辑器，用于查看、试听、修改分句标注结果。

- 用 **Chrome / Edge** 打开即可使用，无需安装、无后端依赖。
- 支持**拖入**方式：把 JSON 和对应音频直接拖进页面即可标注。

## 二、数据格式：segments.json

每个音频对应一个同名的 `segments.json`，结构如下：

```json
{
  "src_audio": "音频文件名.wav",   // 相对路径，与 json 同目录
  "duration": 123.4,              // 音频总时长（秒）
  "segments": [ ... ]             // 分句数组
}
```

`segments` 数组中每一段的字段：

| 字段 | 含义 |
|------|------|
| `id` | 句内序号 |
| `start` / `end` | 该段在音频中的起止时间（秒） |
| `text` | 该段识别文本 |
| `label` | 方言标签：`mandarin`（普通话）/ `guilin`（桂林话）/ `uncertain`（待确认） |
| `score` | 模型初标的置信度（方言分） |
| `signals` | 判别所用特征（声学后验、CER、音变、方言词等） |
| `wav` | （新格式）音频文件名 |

> `src_audio` 为**相对路径**（仅音频文件名），因此 `.wav` 必须与 `.json` 放在**同一目录**，否则编辑器无法定位音频。

## 三、segment_editor.html 使用方法

1. 用 **Chrome / Edge** 打开 `segment_editor.html`；
2. 将 `segments.json` **拖入页面**载入；
3. 将对应的 `.wav` **拖到顶部「已载入」栏**作为试听源（直接绕开路径解析）；
4. 点任意段右侧 ▶ 试听，用下拉框把该段标为 `普通话` / `桂林话` / `待确认`；
5. 点「保存」下载并覆盖原 json。

> 提示：标注前建议先对目录做一份备份（如复制为 `Guilin-dialect-data.bak`），标注结果会直接写回原 json。
