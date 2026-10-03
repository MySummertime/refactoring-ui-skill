# Slim B — 父代理执行说明

在支持独立会话的编码助手里，对 Skill 改动做审计回归。各 case 使用相同模型和推理设置，以便比较结果。

## 一键（报告已经在时）

```bash
# 打分 + 写出汇总页
python3 eval/summarize.py eval/runs/<run-id>
open eval/runs/<run-id>/index.html   # macOS
```

没有报告时，先走下面「派发 8 路」，再跑这一句。

`eval/run.sh <run-id>` 是上面的包装。

## 派发 8 路

对每个 `eval/cases/<id>/` 起一个**新的**子代理，互不共享对话。Prompt = 本文件「硬约束」+ 该 case `expected.json` 的 `prompt` 字段。

硬约束：

```
最多读 3 个文件：
  .agents/skills/refactoring-ui/SKILL.md
  .agents/skills/refactoring-ui/references/13-audit-rubric.md
  eval/cases/<id>/index.html
禁止读 expected.json / CHECKLIST / eval README / PLAN / 其它章节。
禁止开浏览器、起服务、截图。Verified: code-only。
禁止再派子代理。只诊断，不改 fixture。
把完整报告写到 eval/runs/<run-id>/<id>.md 后立刻停。
```

跑完：

```bash
python3 eval/summarize.py eval/runs/<run-id>
```

通过线：汇总页顶栏 **8/8 PASS**。`should` 只作趋势。触发词（A 组）不在这套脚本里。

## 本次目录约定

`eval/runs/auto-2026-08-21/`
