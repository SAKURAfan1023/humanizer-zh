# Humanizer 中文版

让 AI 帮你把中文写得自然、清楚，减少套话和翻译腔，保留事实与作者语气。

这是一个供 AI 助手读取的写作技能（Skill），改编自 [blader/humanizer](https://github.com/blader/humanizer)。它提供编辑规则，由你使用的模型执行；无需额外部署服务或配置本项目专用的 API Key。

## 看一个例子

原文：

> 本周我们围绕导出体验持续发力，完成了导出进度提示的开发，为用户体验提升注入新动能。目前仅在测试环境完成自测，尚未上线；下周计划联调，具体时间待确认。

改稿：

> 本周完成了导出进度提示的开发，并在测试环境完成自测，尚未上线。计划下周联调，具体时间待确认。

这段示例删掉了套话，保留了工作进度、验证范围和后续计划。它是用于说明规则的虚构材料，更多例子见 [中文示例与验收要点](references/examples.md)。

## 适合用在哪里

- 润色工作汇报、产品介绍、技术说明和客户邮件。
- 修改读起来生硬、句式重复或满是空泛评价的中文初稿。
- 根据你提供的写作样本，调整语气和表达节奏。
- 审阅已有文本，或直接编辑指定文件中的正文。

它不判断一篇文章是不是 AI 写的，也不承诺降低检测分数。润色不能代替事实核查；涉及数字、承诺、引用和业务结论时，应对照原始材料复核。

## 中文版改了什么

保留原版“识别问题、改写、复核”的工作方法，重新编写中文规则和示例：

- 处理“持续赋能”“注入新动能”“进行一个优化”等具体语境中的赘述，不把词语设为一律禁止。
- 保留正常中文标点、礼貌表达和省略主语，不照搬英文标点规则。
- 保留“仅”“尚未”“预计”“可能”等限定，防止润色时把计划写成完成、把推测写成事实。
- 默认直接交付改稿；需要时再给对照和解释。
- 文件编辑保留代码、命令、链接目标、元数据和数据值。

完整改编记录见 [来源说明](UPSTREAM.md)。这是独立中文改编版，不是上游官方中文发行版。

## 安装

技能标识为 `humanizer-zh`，界面展示名为“Humanizer 中文版”。安装整个仓库目录，确保 `SKILL.md` 及其引用文件都在，不要只复制入口文件。

### Codex

macOS / Linux，需要 Git：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/SAKURAfan1023/humanizer-zh.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/humanizer-zh"
```

Windows PowerShell，需要 Git：

```powershell
$skillRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $HOME '.codex/skills' }
New-Item -ItemType Directory -Force -Path $skillRoot | Out-Null
git clone https://github.com/SAKURAfan1023/humanizer-zh.git (Join-Path $skillRoot 'humanizer-zh')
```

如果目标文件夹已经存在，先检查是否有本地改动，不要覆盖。安装后在下一轮对话中查看技能列表并调用；如客户端未刷新列表，重新打开会话。

### Claude Code 或其他支持 Skill 的工具

Claude Code 可将仓库克隆到 `~/.claude/skills/humanizer-zh`，项目内使用则放到 `.claude/skills/humanizer-zh`。其他工具按其文档指定的技能目录安装。不同客户端的发现和调用方式可能不同，本项目不包含专用插件安装器。

没有 Git 时，可以在仓库页面选择 **Code → Download ZIP**，解压后将含 `SKILL.md` 的目录重命名为 `humanizer-zh`，放入相应技能目录。不要额外嵌套一层同名文件夹。

## 使用

在 Codex 中显式调用：

```text
请使用 $humanizer-zh 润色下面这段中文。
读者是同事，保持专业、直接，保留所有事实和限定条件，只给改稿。

[粘贴原文]
```

按自己的口吻改写：

```text
请使用 $humanizer-zh。
下面是我的写作样本，仅供参考语气，不要把样本中的经历写进改稿：
[写作样本]

请润色这段文字：
[待改原文]
```

审阅或编辑文件：

```text
请使用 $humanizer-zh 审阅 docs/guide.md，只指出问题，先不要修改文件。
```

```text
请使用 $humanizer-zh 直接润色 docs/guide.md 的中文正文。
保留代码、链接、数据和原有章节结构，完成后简述修改。
```

普通润色默认交付最终稿；需要原文对照时直接说明。要求精简到指定字数时，也请明确哪些信息不能省略。无需先为每次润色提供完整背景表。

## 工作流程与验收

1. 确认读者与编辑边界，识别必须保留的信息。
2. 调整套话、句式和段落，保留原来的语气。
3. 对照原文检查事实、范围、状态和不确定性。
4. 交付改稿；文件任务检查差异，疑点另行说明。

可以用 [示例中的验收要点](references/examples.md) 检查自己的改稿。先确认信息没变，再判断是否好读；不能用“更短了”替代正确性检查。模型表现会有差异，示例不代表所有模型都经过实测。

## 更新与移除

通过 `git clone` 安装且没有本地修改时，可在安装目录运行 `git pull --ff-only`。如果自行修改过技能，先保存改动再合并，避免丢失自己的规则。

通过 ZIP 或技能安装器安装的目录可能不含 Git 信息，不能直接运行 `git pull`。请备份该目录，再下载新版本替换。

不再使用时，将安装目录中的 `humanizer-zh` 文件夹移出技能目录即可。

## 文件说明

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | AI 实际读取的编辑规则 |
| [agents/openai.yaml](agents/openai.yaml) | Codex 中的中文展示名和默认提示 |
| [references/examples.md](references/examples.md) | 中文场景、保留信息和反例 |
| [UPSTREAM.md](UPSTREAM.md) | 上游提交、改编范围和维护方式 |
| [LICENSE](LICENSE) | MIT 许可证及版权声明 |

## 贡献与许可

欢迎通过 Issue 或 Pull Request 提交中文例子和规则改进。请附原文、建议改稿、使用场景和必须保留的信息，使用虚构或脱敏材料，不提交客户资料、内部文档或个人隐私。

本项目使用 MIT 许可证，保留上游作者 Siqi Chen 的版权声明。感谢 [blader/humanizer](https://github.com/blader/humanizer) 提供的编辑框架；详细来源见 [UPSTREAM.md](UPSTREAM.md)。
