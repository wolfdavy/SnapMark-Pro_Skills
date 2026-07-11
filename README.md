# SnapMark

> 截图内容无损转录技能 — 不是 OCR 工具，不是总结工具，而是"截图里有什么，就输出什么"。

## 这是什么

SnapMark 是一个 [Agent Skills](https://agentskills.io) 标准格式的 AI 技能（SKILL.md），让 AI 编码助手在处理截图时遵循**严格无损转录**原则：原样提取正文内容，不总结、不改写、不翻译、不润色、不补充。

## 核心特点

| 特点 | 说明 |
|------|------|
| **零增加** | 不添加标题、编号、解释说明、总结分析等截图中不存在的内容 |
| **零删减** | 正文内容完整保留，不遗漏任何有效信息 |
| **正文优先** | 优先提取正文、邮件、PPT、聊天记录、代码、表格等核心内容 |
| **自动过滤** | 自动跳过水印、浏览器工具栏、任务栏、滚动条、窗口边框等非正文元素 |
| **结构保留** | 保持原始的标题层级、换行、段落、编号、缩进和表格结构 |
| **表格识别** | 清晰表格输出为 Markdown 表格，不清晰时输出纯文本块 |
| **代码保留** | 代码截图保留缩进、空行、注释，禁止自动格式化或优化 |
| **多图有序** | 多张截图严格按输入顺序输出，仅用 `---` 分隔 |
| **模糊标记** | 不确定的内容用 `[unclear]` / `[partially visible]` / `[unreadable]` 标记，禁止猜测 |

## 适用场景

- 微信截图 / 企业微信截图 / 飞书截图 / QQ 截图 → 提取聊天记录
- Teams 截图 → 提取会议对话
- PPT 截图 → 提取幻灯片文字
- Word 截图 → 提取文档内容
- Excel 截图 → 提取表格数据
- 代码截图 → 提取源代码
- 网页截图 → 提取页面正文
- 聊天记录截图 → 转为文本存档

## 使用方法

### 方式一：直接对话

把截图发给已安装 SnapMark 技能的 AI 助手，直接说：

```
请提取这张截图中的内容
```

AI 会自动加载技能并按严格无损转录规则输出。

### 方式二：作为技能调用

在支持技能系统的工具中（如 WorkBuddy、Claude Code），可直接通过技能名调用：

```
/skill snapmark
```

## 安装路径

SnapMark 遵循 [Agent Skills 开放标准](https://agentskills.io)，支持主流 AI 编码助手。将 `SKILL.md` 文件放到对应目录即可：

### 项目级安装（跟随仓库，团队共享）

| AI 工具 | 安装路径 | 说明 |
|---------|---------|------|
| **WorkBuddy** | `.workbuddy/skills/snapmark/SKILL.md` | 原生支持，自动加载 |
| **Claude Code** | `.claude/skills/snapmark/SKILL.md` | 原生支持，按需触发 |
| **GitHub Copilot** | `.github/skills/snapmark/SKILL.md` | 项目级技能目录 |
| **Cursor** | `.cursor/skills/snapmark/SKILL.md` | 项目级技能目录 |
| **Windsurf** | `.windsurf/rules/snapmark.md` | 将 SKILL.md 内容复制为规则文件 |
| **Cline** | `.cline/rules/snapmark.md` | 将 SKILL.md 内容复制为规则文件 |
| **Continue** | `.continue/rules/snapmark.md` | 将 SKILL.md 内容复制为规则文件 |
| **Codex (OpenAI)** | `AGENTS.md` | 将 SKILL.md 内容追加到 AGENTS.md |
| **Gemini CLI** | `GEMINI.md` | 将 SKILL.md 内容追加到 GEMINI.md |
| **Aider** | `CONVENTIONS.md` | 将 SKILL.md 内容追加到 CONVENTIONS.md |
| **Trae** | `.trae/rules/snapmark.md` | 将 SKILL.md 内容复制为规则文件 |

### 用户级安装（个人全局，所有项目生效）

| AI 工具 | 安装路径 |
|---------|---------|
| **WorkBuddy** | `~/.workbuddy/skills/snapmark/SKILL.md` |
| **Claude Code** | `~/.claude/skills/snapmark/SKILL.md` |
| **GitHub Copilot** | `~/.copilot/skills/snapmark/SKILL.md` |
| **Cursor** | `~/.cursor/skills/snapmark/SKILL.md` |

### 安装示例

```bash
# 以 WorkBuddy 为例（项目级）
mkdir -p .workbuddy/skills/snapmark
cp SKILL.md .workbuddy/skills/snapmark/SKILL.md

# 以 Claude Code 为例（用户级，全局生效）
mkdir -p ~/.claude/skills/snapmark
cp SKILL.md ~/.claude/skills/snapmark/SKILL.md

# 以 Cursor 为例（项目级规则）
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/snapmark.md

# 以 GitHub Copilot 为例（追加到指令文件）
echo "" >> .github/copilot-instructions.md
cat SKILL.md >> .github/copilot-instructions.md
```

## 工作原理

SnapMark 采用**渐进式加载（Progressive Disclosure）**机制：

1. **第一层**：YAML frontmatter 中的 `name` 和 `description` 始终在上下文中（约 100 tokens），AI 据此判断是否需要激活
2. **第二层**：当用户发送截图时，AI 加载 SKILL.md 正文（10 项核心原则 + 检查清单）
3. **第三层**：AI 按照原则逐项执行，输出前对照检查清单验证

## SnapMark-Strict 模式

当检测到以下截图类型时，自动启用增强模式：

- 微信 / 企业微信 / Teams / 飞书 / QQ 聊天截图
- PPT / Word / Excel 文档截图
- 代码截图

增强模式下，AI 会最大化保留原始排版、中英文混排格式、换行、缩进、表格布局和代码格式，并自动去除覆盖式水印。

## 许可证

MIT License - 可自由使用、修改和分发。

## 技能标准

本技能遵循 [Agent Skills 开放标准](https://agentskills.io)，兼容支持该标准的所有 AI 编码助手。
