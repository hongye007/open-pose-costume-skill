# Open Pose & Costume Skill

**中文** · [English](README.en.md)

将**姿势＋服饰＋人物**融合成一张人物图的 Codex 技能。人物参考决定身份和画风，姿势参考决定动作，服饰参考决定穿搭。

[浏览参考库](https://hongye007.github.io/open-pose-costume/) · [技能文件](skills/pose-costume-character/SKILL.md) · [下载技能包](https://github.com/hongye007/open-pose-costume-skill/releases/latest)

## 能做什么

- 用人物、姿势、服饰三张参考图生成一张融合图。
- 接受图片、本地文件、可访问的图片链接和明确的文字描述。
- 按 Open Pose & Costume 的编号或关键词选择姿势和服饰，如 `P047`、`SPR-0050`。
- 分别约束人物五官与发型、动作支撑点、服装版型与材质，避免把人偶线条或服装模特的脸带入结果。
- 检查实际生成图，保存并展示结果。

## 安装

在 Codex 中发送：

> 使用 skill-installer，从 hongye007/open-pose-costume-skill 安装 skills/pose-costume-character。

也可使用 Codex 自带安装器（macOS / Linux）：

```sh
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --repo hongye007/open-pose-costume-skill \
  --path skills/pose-costume-character
```

安装后重启 Codex，使技能被发现。已有同名技能时，先备份旧版本再更新；不要重复复制到旧目录内。

[发布页](https://github.com/hongye007/open-pose-costume-skill/releases/latest) 同时提供 `.skill` ZIP 包，内含 `pose-costume-character/`。解压后将该文件夹放入 `$CODEX_HOME/skills/`（默认 `~/.codex/skills/`）即可。

## 使用

上传三张图片后：

```text
使用 $pose-costume-character：
图一是人物，图二是姿势，图三是服饰。
保留人物的脸、发型和画风，采用指定姿势和穿搭，生成一张完整人物图。
```

用参考库编号搭配人物图：

```text
使用 $pose-costume-character，人物用我上传的照片，
姿势 P047，服饰 SPR-0050，保留人物脸和发型。
```

也可以用文字：

```text
使用 $pose-costume-character：
人物是黑色短发的成年女性，侧坐、单臂上举，
穿米色开衫和白色长裤，生成一张插画。
```

默认生成一张图。人物只有文字时，会依描述创造人物；人物图片则用于约束已有身份。实际结果取决于模型和输入质量。

## 生图能力与配置

需要运行环境提供多图参考生图能力。默认使用 Codex 可用的内置图像工具，并遵循环境中的 `imagegen` 技能指引。仓库提供工作流程和提示词模板。

明确选择兼容 API 时，默认模型为 `gpt-image-2`；选择 Atomflow 时服务预设为 `https://atomflow.vip/v1`。服务地址、模型与凭证由当前任务和本地配置决定。API Key 应留在本机环境变量或受信任配置中，生成费用以服务商为准。

只有两张图片、人物使用文字描述时，提交两张参考图；三种输入均为图片时，提交三张参考图。技能会标明实际图片顺序与用途。

## 文件结构

```text
skills/pose-costume-character/
├── SKILL.md                         # 工作流程与输入职责
├── agents/openai.yaml               # Codex 展示与调用信息
└── references/
    ├── gallery.md                   # 按编号／关键词接入参考库
    └── prompt-template.md           # 三参考融合提示词模板
```

技能通过公开索引解析所选参考，只读取需要的素材。图片服务不可用或缺少生图能力时会说明阻塞，不会把提示词当作已生成的图片交付。

## 授权与来源

本仓库的原创技能文档和模板使用 [MIT 许可](LICENSE)。人物图片、参考库素材与外部服务保留各自权利。参考库图片及完整元数据未打包进仓库；相关使用限制见 [SOURCES.md](SOURCES.md)。

相关项目：[Open Pose & Costume](https://github.com/hongye007/open-pose-costume) · 作者 X：[HongyeMain](https://x.com/HongyeMain)
