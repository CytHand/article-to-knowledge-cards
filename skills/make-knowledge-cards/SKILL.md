---
name: make-knowledge-cards
description: Turn pasted articles or local Markdown/TXT files into 5-8 source-grounded knowledge cards. Use when the user wants to extract, summarize, or study the key knowledge from one article or local text file.
---

# Make Knowledge Cards

Convert one source into concise knowledge cards. Aim for 5-8 cards, but never pad the result. If the source supports fewer distinct, important points, return only those cards and briefly state that the source was too limited to justify more.

## Supported Inputs

- Text pasted directly by the user.
- One local `.md`, `.markdown`, or `.txt` file.

Do not fetch web pages or process PDFs. Do not create Anki decks or a graphical interface. If the request depends on one of those capabilities, explain that it is unsupported and ask for pasted text or a local Markdown/TXT file instead.

## Workflow

1. Read the complete source before selecting content. Preserve its meaning, terminology, qualifications, and uncertainty. Do not add outside facts or infer missing details.
2. Preserve scope and certainty: keep examples as examples and observations as observations. Do not turn an anecdote, sequence of events, or correlation into a general causal rule unless the source states that conclusion.
3. Extract candidate knowledge units: central claims, definitions, mechanisms, causal relationships, distinctions, conditions, exceptions, procedures, evidence, and practical warnings.
4. Remove repeated or near-duplicate units. Merge only material that expresses the same single knowledge point.
5. Rank the remaining units by importance to the source's purpose, not by how interesting or vivid they sound.
6. Select 5-8 units when enough distinct material exists. Otherwise select fewer. Do not split one point across cards merely to reach a target count, and do not invent filler.
7. Draft one card per selected unit using the output format below.
8. Review every card against the source and the quality checks before responding.

## Card Requirements

- **Title:** A short, specific label that identifies the knowledge point.
- **Core knowledge:** One sentence stating the single point the card teaches.
- **Concise explanation:** One to three sentences that clarify the point without introducing new facts.
- **Example or self-test:** Prefer an example actually present in the source. If none is suitable, write a self-test question whose answer is explicitly supported by the source and that tests this card's point. Never invent an example.

## Output Format

Write in the source's language unless the user requests another language. Localize the card labels and heading to that language. For Chinese sources, use:

```markdown
## 知识卡片 1：标题

**核心知识：** 一句话。

**简明解释：** 一至三句话。

**例子 / 自测：** 原文中的例子，或可由原文回答的问题。
```

For other languages, translate the labels and heading while keeping the same field order.

If the source supports fewer than five cards, add one short note after the cards, such as: `原文信息有限，仅提取到 3 张卡片，未强行补充。`

## Quality Checks

- Every card contains exactly one knowledge point.
- Cards do not repeat or substantially overlap.
- The highest-value points from the source are represented within the 5-8 card limit.
- Every factual statement is directly supported by the source.
- Claims retain the source's scope; a case observation is not presented as a universal causal rule.
- Examples are source-grounded, and each self-test question is answerable from and focused on its own card's point.
- The response contains only supported cards; no unsupported claims, generic advice, or invented details.