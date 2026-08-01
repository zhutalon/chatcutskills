# ChatCut 主题口播精剪 Skill

这是一个可复用的 Codex Skill。给它一组口播视频，并可选提供主题、截图、参考图片或参考视频，它会调用 ChatCut 完成：

- 按文件编号编排多段视频
- 删除语气词、口误、停顿和重复内容
- 从原始表达中提炼开头钩子
- 收集、生成并整理补充视觉素材
- 将用户提供的截图和参考素材导入 ChatCut，并实际放到时间轨道
- 制作以中文为主的文字说明和视觉包装
- 验证成片节奏、画面、音频与素材使用情况
- 默认交付可继续编辑的 ChatCut 工程

Skill 目录是 `chatcut-topic-video-editor/`，调用名称是 `$chatcut-topic-video-editor`。

## 使用前提

- 使用支持 Skills 的 Codex 环境
- 已安装并连接 ChatCut 插件
- Codex 能够读取你提供的本地或附件素材
- 已把本仓库中的 Skill 安装到 Codex 的 Skills 目录

## 安装

克隆或下载本仓库后，把 `chatcut-topic-video-editor` 复制到 Codex 的 Skills 目录：

```bash
cp -R chatcut-topic-video-editor ~/.codex/skills/
```

也可以创建软链接，方便直接在 Git 仓库里维护和更新：

```bash
ln -s /你的绝对路径/chatcutskills/chatcut-topic-video-editor \
  ~/.codex/skills/chatcut-topic-video-editor
```

如果设置了 `CODEX_HOME`，请改用 `$CODEX_HOME/skills/`。安装后重新打开 Codex 任务，确保 Skill 出现在可用 Skills 列表中。

## 最小调用示例

在 Codex 中发送：

```text
使用 $chatcut-topic-video-editor

视频：
- /path/to/1.mp4
- /path/to/2.mp4

主题：让 AI 操作专业软件完成任务
顺序：按文件编号
交付：先完成 ChatCut 可编辑版本，暂不导出
```

只要明确写出 `使用 $chatcut-topic-video-editor`，并提供视频路径或附件，就可以启动完整流程。

## 附带截图和参考素材

除了视频，还可以一起提供软件截图、产品界面、Logo、图片、GIF、SVG、参考视频或文档：

```text
使用 $chatcut-topic-video-editor

视频：
- /path/to/1.mp4
- /path/to/2.mp4

配图和参考素材：
- /path/to/product-ui.png（must-use）
- /path/to/result-before-after.jpg（must-use）
- /path/to/design-reference.png（style-only）
- /path/to/reference-demo.mp4（must-use，用作 B-roll）

主题：用 ChatGPT 指挥 OnyX 清理 macOS
视觉：米白网格手账，新增文字以中文为主
目标：YouTube 横屏 16:9，节奏紧凑
交付：ChatCut 可编辑版本，确认后再导出 MP4
```

素材标签的含义：

- `must-use`：必须导入，并实际放到时间轨道中
- `style-only`：只用于参考设计风格，不要求出现在成片里
- `alternate`：候选素材，由 Skill 选择更合适的一份使用
- `blocked`：素材无法安全读取、格式不支持或不适合使用；交付时会说明原因

如果没有给截图或参考素材标注用途，Skill 会默认按 `must-use` 处理。

## 可以补充的要求

你可以在调用时继续指定：

- 视频顺序和需要保留或删除的片段
- 目标平台、画幅和预计时长
- 主题、核心观点和开头钩子的方向
- 视觉风格、品牌色、字体与中文用字偏好
- 每份素材出现的大致位置或用途
- 是否需要字幕、背景音乐、音效、封面或导出文件

没有指定时，Skill 会采用适合中文知识型口播的稳妥默认设置。

## 默认工作方式

- 多段视频优先按文件名中的数字顺序编排
- 先完成口播主线精简，再放置截图、B-roll 和文字包装
- 用户提供的素材优先于搜索或生成的替代素材
- 素材仅导入媒体库不算完成，必须按用途放到时间轨道
- 新增说明文字以中文为主；软件原生界面文字保持原样
- 钩子优先从原始内容中提炼，不虚构讲者没有表达过的结论
- 默认不擅自添加音乐、字幕或复杂特效
- 默认交付可编辑的 ChatCut 工程；只有明确要求时才导出 MP4
- 交付报告会列出已使用和未使用的用户素材，并说明原因

## AI 生成图片的默认风格

- `chatcut-topic-video-editor/assets/generated-image-style/` 中的六张内置参考图，只作为 AI 生成补充静帧的默认风格锚点。
- 真实截图和可编辑的中文文字／Motion Graphics 不继承这些参考图的插画风格。
- 如果任务明确指定了生成图片的风格，应以该任务级风格覆盖内置默认风格。

## 预期交付

流程完成后，Codex 会返回：

- 可打开的 ChatCut 工程
- 精剪后的大致时长
- 删除和重组内容的摘要
- 钩子、截图、B-roll 和文字包装的使用说明
- 用户提供素材的使用清单
- 时间轨道、画面和音频验证结果
- 导出状态；未要求导出时会明确说明

## 仓库结构

```text
chatcutskills/
├── README.md
└── chatcut-topic-video-editor/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   └── generated-image-style/
    └── references/
        ├── editorial-workflow.md
        ├── visual-assets.md
        ├── chatcut-operations.md
        └── quality-checklist.md
```

## 一句话调用模板

```text
使用 $chatcut-topic-video-editor，把我提供的视频按编号合并精剪；结合主题删除语气词和重复内容，提炼开头钩子，并把所有未标注用途的截图和参考素材按 must-use 导入并放到 ChatCut 时间轨道。新增文字以中文为主，先交付可编辑工程，不要直接导出。
```
