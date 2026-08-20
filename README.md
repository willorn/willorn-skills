<div align="center">

# Willorn Skills

我自己在用的一些 AI Skill，开源在这里。

[![License](https://img.shields.io/badge/License-MIT-3B82F6?style=for-the-badge)](./LICENSE)
[![Skills](https://img.shields.io/badge/Skills-1-10B981?style=for-the-badge)](#-skills)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-8B5CF6?style=for-the-badge)](https://agentskills.io)

</div>

这里的每个 Skill 都遵循 [Agent Skills](https://agentskills.io) 开放标准。Claude Code、Codex 等支持该标准的 Agent 都能安装使用。

---

## 目录

| 名字 | 一句话 |
|---|---|
| 🧠 [**truth-of-thinking**](#-truth-of-thinking) | 用「定义 → 分类 → 比较 → 因果」把概念、决策、流程想清楚 |

---

## 安装方式

在 Claude Code、Codex 等支持 Agent Skills 的工具里，直接说：

```text
帮我安装这个 skill：https://github.com/willorn/willorn-skills/tree/main/<skill-name>
```

把 `<skill-name>` 换成你想装的那个，例如 `truth-of-thinking`。Agent 会自己放到对应目录。

你的 Agent 不支持 Skill 也没关系：把对应目录的 `SKILL.md` 全文下载下来，当成项目规则文件（或直接贴进对话）让 Agent 照着执行即可。

---

## Skills

<a id="-skills"></a>

### 🧠 truth-of-thinking

用四个基本动作作为默认思考顺序：

```text
定义 -> 分类 -> 比较 -> 因果
```

适合澄清概念、做决策、设计流程 / SOP，或把学习沉淀成可复用笔记。决策、工作流、关系、类比、迭代都是这四个动作的应用或延伸，不另起一套花架子。

→ [SKILL.md](./truth-of-thinking/SKILL.md)

---

## License

[MIT](./LICENSE)
