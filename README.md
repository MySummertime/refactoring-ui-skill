# Refactoring UI Skill

[English](README.en.md)

这是一个供编码助手使用的网页界面设计 Skill。它把常见的设计检查工作组织成可按需读取的规则、案例和脚本，帮助助手在编写界面、调整样式或评审页面时给出有依据的建议。

## 项目来源

本仓库改编自 [Edison Li 的 refactoring-ui-skill](https://github.com/edisonmbli/refactoring-ui-skill)。原项目采用 MIT 许可证；本仓库保留其 [LICENSE](LICENSE) 中的版权声明，并在现有基础上调整了 Skill 的目录和跨工具使用说明。当前版本由 [MySummertime](https://github.com/MySummertime) 维护。

设计原则来自 Adam Wathan 和 Steve Schoger 的 [《Refactoring UI》](https://www.refactoringui.com/)。本项目并非原书或原项目的官方版本，也未获得上述作者的认可。想系统学习这些原则，建议阅读原书；关于来源和使用边界，另见 [ATTRIBUTION.md](ATTRIBUTION.md)。

## 适用场景

- **构建界面：** 在动手写页面前梳理内容层级、布局、排版与组件状态。
- **改进现有页面：** 根据项目已有的设计体系定位不协调的间距、颜色、对比度和视觉重点。
- **设计评审：** 将发现的问题按严重程度排列，附上对应规则编号和可执行的修改建议。
- **建立设计 Token：** 在缺少统一约定时生成基础色板与 Token，并检查文本对比度。
- **解释设计决定：** 查询某条原则的原因、适用条件和常见误用。

Skill 会先检查项目的技术栈及现有 Token，再选择合适的建议。它支持普通 CSS、Tailwind 和常见组件库；不会自行替换项目已有的设计体系。能预览页面时，应结合实际渲染结果评审；仅能读取代码时，需要标明视觉结论尚未验证。

## 安装

唯一的 Skill 目录是 [`.agents/skills/refactoring-ui/`](.agents/skills/refactoring-ui/)。在支持项目级 Agent Skills 的 Codex 或 VS Code 助手中打开本仓库，可以直接使用它。

要在另一个项目中使用，请在**目标项目根目录**执行：

```bash
skill_checkout=$(mktemp -d)
git clone --depth 1 git@github.com:MySummertime/refactoring-ui-skill.git "$skill_checkout/repo"
mkdir -p .agents/skills
cp -R "$skill_checkout/repo/.agents/skills/refactoring-ui" .agents/skills/
rm -rf "$skill_checkout"
```

如果本仓库已经克隆到别处，把最后一行的源路径改为实际位置即可。个人使用可以复制到 `~/.agents/skills/`；其他支持 Agent Skills 的工具可使用其认可的 Skill 目录，例如 Claude Code 的项目级 `.claude/skills/`。每个作用域保留一份副本，以免重复发现。如果助手没有自动发现 Skill，可参考 [`templates/AGENTS.md`](templates/AGENTS.md) 添加明确的入口说明。

## 如何使用

安装后，用正常语言提出任务即可。例如：

> 检查这个设置页在手机和桌面宽度下的层级、间距和对比度，按严重程度列出问题，并指出对应规则。

> 这个项目还没有设计 Token。请先检查现有样式，再提出一套能融入当前技术栈的基础方案。

> 改进这个空状态，同时保留项目当前的组件和颜色约定。

评审结果应区分可从源码确认的问题和必须看实际页面才能确认的问题。若某种视觉选择是有意为之，可以在任务中说明，让助手把它当作项目约束。

## 仓库内容

| 路径 | 用途 |
| --- | --- |
| [`.agents/skills/refactoring-ui/SKILL.md`](.agents/skills/refactoring-ui/SKILL.md) | 任务路由和核心工作流程 |
| [`.agents/skills/refactoring-ui/references/`](.agents/skills/refactoring-ui/references/) | 按主题读取的设计规则与评审依据 |
| [`.agents/skills/refactoring-ui/scripts/`](.agents/skills/refactoring-ui/scripts/) | 色板生成、对比度检查和 Token 输出 |
| [`.agents/skills/refactoring-ui/assets/`](.agents/skills/refactoring-ui/assets/) | 可复用的模板 |
| [`eval/`](eval/) | 评测案例与评分工具 |

Skill 由 Markdown 和 Python 3.9+ 脚本组成，不要求安装第三方 Python 包。具体的 Skill 发现方式可能随工具版本变化，请以所用工具的当前文档为准。

## 许可

本仓库遵循 [MIT 许可证](LICENSE)。改编来源、原书与本仓库之间的关系见 [项目来源](#项目来源) 和 [ATTRIBUTION.md](ATTRIBUTION.md)。
