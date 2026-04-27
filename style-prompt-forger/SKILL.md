---
name: style-prompt-forger
description: Reverse-engineer reusable image-generation style prompts from reference images, design styles, Pinterest/X/art references, or user aesthetic examples through a Gemini-to-GPT browser workflow. Use when the user invokes @style-prompt-forger or asks to extract visual style, create a reusable "焚诀", generate images from a reference style, or refine GPT image prompts while avoiding generic AI-image aesthetics.
---

# Style Prompt Forger

Create a reusable style prompt ("焚诀") from a reference image, then use that prompt in GPT image generation. The intended user flow is: `@style-prompt-forger` plus an image plus the desired new subject.

## Source Reference

This skill was inspired by the Bilibili video "GPT焚决？给你反推焚决的焚决！基于 Gemini + GPT 的提取风格+生图的生图流程" by 咲凌_Arisa: https://www.bilibili.com/video/BV1eKojBkE5e/

## Done Definition

The workflow is complete when Gemini has produced a reusable Chinese 焚诀, GPT has used that 焚诀 to generate or prepare the requested image, and the final output preserves transferable style while removing the source image's concrete subject, IP, text, and story.

## Use Boundaries

Use when:
- The user invokes `@style-prompt-forger` with a reference image and target subject.
- The user wants to reverse-engineer a visual style into a reusable image prompt.
- The user asks for a custom "焚诀" instead of copying public prompt recipes.
- The user wants Gemini to extract style and GPT to generate from that extracted prompt.

Do not use when:
- The user only wants a direct image and does not need a reusable style prompt.
- The request asks to replicate a living artist's style, copyrighted character, logo, or exact protected work.
- The user asks for credential entry, payment actions, account settings, or private browser-tab automation.

## Execution Contract

- Capability requirements: image understanding, prompt synthesis, and browser automation delegated to the installed browser-control skill.
- Harness/tool assumptions: reuse the Hermes `agent-browser` skill when installed, commonly at `$HOME/.hermes/hermes-agent/node_modules/agent-browser/skills/agent-browser/SKILL.md`, configured with Chrome/Chromium DevTools Protocol port `9222`.
- Environment binding: Chrome/Chromium must already be running with remote debugging port `9222`; Gemini and ChatGPT/GPT image UI must already be logged in.
- Fixed model roles: Gemini extracts and revises the 焚诀; GPT only consumes the 焚诀 to generate the image.
- Parallelism boundaries: browser preflight may prepare Gemini and GPT tabs in parallel; the core DAG is sequential: Gemini extract -> GPT generate -> evaluate -> optional Gemini revise -> GPT regenerate.
- Reusable references: read `references/reverse-style-template.md` for the Gemini extraction prompt and `references/refinement-rules.md` for iteration failures.
- Failure handling: if port `9222` is unreachable, report the browser preflight failure; if login is missing, ask the user to log in manually; if GPT output is generic or off-style, return to Gemini for a revised 焚诀.
- Verification: the Gemini prompt must include `[在此处替换为您想要生成的主体内容]`, strip source-specific content, and be reusable by replacing only the placeholder.

## Browser Skill Delegation

Do not reimplement browser-control instructions inside this skill. Invoke the installed Hermes browser-control skill as the execution harness:

- Preferred skill: Hermes `agent-browser`
- Skill path: `$HOME/.hermes/hermes-agent/node_modules/agent-browser/skills/agent-browser/SKILL.md`
- Preferred command: `npx agent-browser --cdp 9222 ...`
- Fallback command: `agent-browser --cdp 9222 ...` when the global binary exists
- Fixed endpoint: `http://127.0.0.1:9222`
- Required sites: Gemini at `https://gemini.google.com/`, GPT at `https://chatgpt.com/`
- Not the target: `camoufox-browser`, because that skill runs a separate browser service on port `9377`, while this workflow must use the user's existing Chrome on `9222`.

The browser skill owns navigation, snapshots, element refs, uploads, form filling, waiting, screenshots, and tab/session handling. This skill owns only the Gemini -> GPT task graph and prompt artifacts.

## Runtime DAG

1. Preflight browser.
   - Load the Hermes `agent-browser` skill if browser operation details are needed.
   - Use `npx agent-browser --cdp 9222` or `agent-browser --cdp 9222` to connect through `http://127.0.0.1:9222`.
   - Reuse or open Gemini and GPT tabs through that browser skill.
   - Confirm both pages are logged in and ready for prompt input.

2. Gemini extracts the 焚诀.
   - Send the reference image and the extraction prompt from `references/reverse-style-template.md`.
   - Require Gemini to output only one complete Chinese prompt.
   - Require the placeholder `[在此处替换为您想要生成的主体内容]`.

3. GPT generates the image.
   - Replace the placeholder with the user's target subject.
   - Send the resulting prompt to GPT image generation.
   - Do not ask GPT to reinterpret or merge style analysis; GPT's role is generation.

4. Evaluate the result.
   - Pass if style transfer is clear, subject is correct, and the result does not copy source-specific content.
   - If it fails, classify the failure using `references/refinement-rules.md`.

5. Revise through Gemini.
   - Send Gemini the original reference, current 焚诀, GPT result or failure description, and the requested correction.
   - Ask Gemini to revise the 焚诀 only.
   - Return to GPT generation.

## Output Rules

- Return the final reusable 焚诀 and the generated-result status.
- Keep the final prompt in Chinese unless the user asks otherwise.
- Do not expose browser cookies, auth state, unrelated tab content, or private account data.
- Do not present Gemini and GPT answers as merged alternatives; Gemini owns prompt extraction, GPT owns image generation.

## Eval Cases

- Explicit positive: `@style-prompt-forger` plus a poster image: "提取这张图的风格，主体换成一辆复古跑车。"
- Implicit positive: "用 Gemini 帮我从这张图反推焚诀，然后去 GPT 生图。"
- Iteration positive: "这次 GPT 生出来太 AI 味了，回去让 Gemini 改焚诀再生成。"
- Negative control: "直接生成一张赛博猫图。" Use direct image generation instead.
