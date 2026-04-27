# Refinement Rules

Use these rules after GPT generates an image from the Gemini 焚诀.

## Failure Mapping

Generic AI look:
- Add specific era, medium, print process, camera/rendering vocabulary, and layout grammar.
- Replace vague words like "高级感", "精美", "电影感" with concrete visual properties.

Subject drift:
- Strengthen the placeholder replacement with explicit subject identity, pose, scale, and required visible features.
- Ask Gemini to reduce style dominance and preserve subject recognizability.

Style not visible:
- Ask Gemini to move the strongest style cues earlier in the prompt.
- Add medium/material/color/composition constraints instead of adding more adjectives.

Source copied too closely:
- Remove concrete costume, character traits, scene objects, text, logos, and unique layout identifiers.
- Keep only transferable composition, color, texture, and lighting logic.

Text or logo artifacts:
- Add "无文字、无 logo、无水印、无品牌标识" unless the user explicitly wants typography.
- If typography is desired, specify abstract typography treatment without copying source text.

Overcrowded result:
- Add information-density limits, negative space requirements, and subject hierarchy.

Flat result:
- Add perspective, foreground/midground/background layering, lighting direction, material contrast, and focal hierarchy.

## Revision Prompt Back To Gemini

```text
这是你刚才提取的焚诀：
[粘贴当前焚诀]

GPT 根据它生成后的问题是：
[粘贴问题描述，必要时附生成图]

请基于原始参考图和上述问题，只修订焚诀，不要输出分析过程。
保留占位符：[在此处替换为您想要生成的主体内容]
强化风格迁移，删除具体主体/IP/文字/剧情泄漏。
```
