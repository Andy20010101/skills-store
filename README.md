# 🛒 Andy20010101 Skills Store

> OpenClaw Skills & Agents 商店 — Monorepo

这里是所有自建 OpenClaw Skill 的发布源，每个子目录是一个独立技能包，可直接在 OpenClaw 中安装使用。

---

## 📦 已上架技能

### 🤖 boss-zhipin-agent
**BOSS 直聘值班化招聘助手**

定时处理主动应聘消息 + 主动搜索候选人，通过浏览器自动化完成初筛和第一句话发送。

| 属性 | 值 |
|------|-----|
| 触发词 | 启动招聘值班 / 开始BOSS值班 / 我要招人了 / 启动boss-zhipin-agent |
| 定时 | 每30分钟处理消息 · 每2小时主动搜索 |
| 依赖 | web-access |
| 状态 | ✅ 运营中 |

📂 [技能目录](./boss-zhipin-agent/) · [详细文档](./boss-zhipin-agent/SKILL.md)

---

### 🏭 1688-platform-skill
**1688 供应商发现与初筛 Skill**

面向单一产品方向的低频、浏览器优先 1688 供应商研究工作流，输出带可见证据、判断、未知项和来源链接的 Markdown shortlist。

| 属性 | 值 |
|------|-----|
| 触发词 | 1688-supplier-discovery / 启动1688供应商发现 / 1688供应商初筛 |
| 定位 | 单产品方向供应商研究 |
| 依赖 | browser navigation · visible page reading · markdown output |
| 状态 | ✅ 已收录 |

📂 [技能目录](./1688-platform-skill/) · [详细文档](./1688-platform-skill/SKILL.md)

---

### 🎨 style-prompt-forger
**Gemini + GPT 图片风格焚诀提取 Skill**

从参考图中反推可复用中文生图 Prompt，再替换主体交给 GPT 生图；适合海报、插画、设计稿等图像风格迁移工作流。

| 属性 | 值 |
|------|-----|
| 触发词 | @style-prompt-forger / 提取焚诀 / 反推图片风格 / Gemini 提取 GPT 生图 |
| 定位 | 参考图风格提取与新主体生图 |
| 依赖 | Gemini · ChatGPT · agent-browser · Chrome DevTools 9222 |
| 状态 | ✅ 已收录 |

📂 [技能目录](./style-prompt-forger/) · [详细文档](./style-prompt-forger/SKILL.md) · [中文案例](./style-prompt-forger/README.md)

---

## 🚧 即将上线

| 技能 | 描述 | 状态 |
|------|------|------|
| finance-assistant | 财务助手 | 🔲 规划中 |
| procurement-assistant | 采购助手 | 🔲 规划中 |
| business-assistant | 业务助手 | 🔲 规划中 |
| development-assistant | 开发助手 | 🔲 规划中 |
| document-assistant | 单证助手 | 🔲 规划中 |

---

## 📦 安装方式

从 GitHub 直接安装到 OpenClaw：

```bash
openclaw skills install Andy20010101/skills-store/boss-zhipin-agent
openclaw skills install Andy20010101/skills-store/1688-platform-skill
openclaw skills install Andy20010101/skills-store/style-prompt-forger
```

或通过 [ClawhHub](https://clawhub.com) 搜索 `boss-zhipin-agent`。

---

## ➕ 添加新技能

1. 在本仓库根目录创建新目录，命名格式：`{领域}-assistant` 或 `{功能}-skill`
2. 目录内必须有 `SKILL.md`（技能说明）
3. 可选：`references/`（详细参考文档）、`job-packages/`（岗位包配置）
4. 提交 PR 或直接 push，主仓库维护者审核后合并

---

*Last updated: 2026-04-27*
