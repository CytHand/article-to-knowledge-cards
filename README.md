# make-knowledge-cards

一个用于把文章或本地 Markdown/TXT 文件提炼成 5～8 张知识卡片的开源 Skill。它适合学习、复习和整理长文，每张卡片都包含标题、核心知识、简明解释，以及源自原文的例子或自测问题。

## 1. 项目解决什么问题

阅读文章后，重要内容往往分散在多个段落中，还可能夹杂重复、例子和次要信息。手动整理时容易遗漏重点、重复记录，或者补充原文没有的结论。

`make-knowledge-cards` 帮助用户从一篇文章或一个本地文本文件中提取真正重要的知识，将内容整理成结构统一、便于复习的卡片，同时保持信息可追溯，不编造原文之外的细节。

## 2. 主要功能

- 支持用户直接粘贴文章，或读取本地 `.md`、`.markdown`、`.txt` 文件。
- 默认提炼 5～8 张知识卡片；原文信息不足时只生成能够支撑的卡片，不强行凑数。
- 每张卡片包含标题、核心知识、简明解释，以及例子或自测问题。
- 一张卡片只讲一个知识点，并删除重复或高度重叠的内容。
- 优先保留原文的重要观点、定义、机制、条件、步骤和提醒。
- 默认使用原文语言输出；用户要求其他语言时，卡片标题和字段也会切换为该语言。
- 不补充原文没有的信息。原文没有合适例子时，改为出可由原文回答的自测问题。
- 不依赖脚本、外部程序或第三方库。

暂不支持网页抓取、PDF、Anki 和图形界面。

## 3. 安装方法

本 Skill 的安装过程就是把技能目录复制到 Codex 可以发现的位置，不需要安装依赖或运行构建命令。

项目内的技能目录为：

```text
skills/
└── make-knowledge-cards/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

### 在 macOS 或 Linux 上安装到用户级技能目录

在项目根目录运行：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/make-knowledge-cards "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### 在 Windows PowerShell 中安装到用户级技能目录

在项目根目录运行：

```powershell
$codexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$skillsRoot = Join-Path $codexHome 'skills'
New-Item -ItemType Directory -Force -Path $skillsRoot | Out-Null
Copy-Item -Recurse -Force '.\skills\make-knowledge-cards' $skillsRoot
```

安装后，Codex 可以在用户技能目录中读取 `make-knowledge-cards/SKILL.md` 和 `make-knowledge-cards/agents/openai.yaml`。

## 4. 使用方法

在支持 Skill 的 Codex 环境中调用 `$make-knowledge-cards`，然后粘贴文章或提供本地文件路径。

粘贴文章：

```text
$make-knowledge-cards

[在这里粘贴文章]
```

读取本地 Markdown 或 TXT 文件：

```text
$make-knowledge-cards 请把 ./notes/example.md 转化为知识卡片。
```

如果希望使用与原文不同的语言输出，可以在请求中说明：

```text
$make-knowledge-cards 请把 ./notes/example.md 转化为中文知识卡片。
```

输出卡片数量会根据原文内容决定：素材足够时生成 5～8 张；有效知识点不足时返回较少卡片，并说明原文信息有限。

## 5. 输入与输出示例

### 输入

```text
番茄在未完全成熟时采摘，可以在室温下继续成熟。低温会减慢成熟过程，
因此尚未成熟的番茄不宜立即放入冰箱。成熟后，低温储存可以延缓进一步
软化。将番茄与香蕉等释放乙烯的水果放在一起，可以加快成熟。
```

### 可能输出

```markdown
## 知识卡片 1：未成熟番茄可后熟

**核心知识：** 未完全成熟的番茄采摘后仍可在室温下继续成熟。

**简明解释：** 原文将室温描述为未成熟番茄继续成熟的条件。

**例子 / 自测：** 为什么未完全成熟的番茄采摘后不一定要马上食用？

## 知识卡片 2：低温会减慢成熟

**核心知识：** 低温会减慢番茄的成熟过程。

**简明解释：** 因此，尚未成熟的番茄不宜立即放入冰箱。

**例子 / 自测：** 尚未成熟的番茄为什么不宜立即冷藏？

## 知识卡片 3：成熟后适合低温储存

**核心知识：** 番茄成熟后可以用低温延缓进一步软化。

**简明解释：** 低温的作用会随成熟阶段变化：未成熟时它会减慢成熟，成熟后则可延缓软化。

**例子 / 自测：** 番茄成熟后冷藏的主要作用是什么？

## 知识卡片 4：乙烯可加快成熟

**核心知识：** 香蕉等释放乙烯的水果可以加快番茄成熟。

**简明解释：** 原文建议将番茄与这类水果放在一起，以加快成熟。

**例子 / 自测：** 原文给出了哪一种加快番茄成熟的方法？

原文信息有限，仅提取到 4 张卡片，未强行补充。
```