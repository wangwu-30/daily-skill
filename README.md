# daily-skill：个人 AI 日报 Skill（Personal AI Daily）

[中文](#中文) · [English](#english)

## 中文

**把这句话发给你的 agent：**

> 读 https://github.com/wangwu-30/daily-skill 的 SKILL.md 和 ACCEPTANCE.md，按它帮我搭一份个人 AI 日报：先问我关注什么、信任哪些人和来源、偏好什么风格，其余全部由你完成。

这是一份写给 Agent 的规范（白皮书），**不提供任何程序**，也没有模板仓库。对世界的判断留给你，落地交给 agent。

### 你只需要告诉 agent 三件事

1. **关注什么**：话题和优先级。
2. **信任哪些人和来源**：人、账号、网站、社媒都可以。
3. **偏好什么风格**：语言、时区、栏目、长短和口吻。

建仓、写代码、配置定时发布（如 GitHub Actions + Pages）、用 `ACCEPTANCE.md` 自检并修复，都由 agent 照 skill 完成。它需要你授权时（例如 `gh auth login`、可选的模型 API key）会直接问你。

参考实例：https://www.wangwu.ai/daily/

### 加入黄页（可选）

黄页收录的是每个人**自己的日报网站**（经过收集、重排、发布后的产物），不是源清单；OPML 源清单只是可选项。默认不加入。想加入时对 agent 说一句：

> 把我的日报加入黄页 https://github.com/wangwu-30/ai-digest-registry

agent 会 fork 黄页仓库、写好条目、开 PR（SKILL.md §5）。准入只看三项：条目合法、站点现在能访问、最近 14 天内有更新。

### 接入新的来源（包括小红书、即刻等社媒）

告诉 agent「把小红书上的某某也作为来源」即可。下面是 agent 照着做的约定：采集层是可插拔的适配器（SKILL.md §4.2a），类型不限于 RSS。

1. 在 `config/sources.yaml` 里加一条，社媒用 `type: social` 加 `platform`：
   ```yaml
   - {id: xhs-people, type: social, platform: xiaohongshu, accounts: ["<用户 id>"], lane: followed, topic: agents}
   - {id: jike-ai, type: social, platform: jike, query: "AI Agent", lane: discover, topic: agents}
   ```
   全新的类型先命名为 `x-<名字>`（如 `x-wechat-mp`）。
2. 让 Agent 按 §4.2a 写一个适配器：实现 `validate`、`fetch`（返回 `{url, title, published_at, author, text, metrics, kind}`），注册到这个 type/platform 下。后面的去重、排序、摘要、发布不用改。
3. 没有公开接口的平台，可以读你自己导出的收藏、遵守 robots 的公开页面，或你自己跑的桥接（如 RSSHub，此时直接用 `type: feed`）。**不要把自己的登录 cookie 放进公开的 workflow。**
4. 跑一次，确认没有 `no_adapter` / 失败日志，ACCEPTANCE 自检通过。

### 目录结构

```
SKILL.md                     规范正文（给 Agent 读）
ACCEPTANCE.md                验收标准（R 层：公开 URL 可验证；S 层：仓库内自证）
schema/
  digest.v1.3.json           每期 data.json 的当前格式
  digest.v1.2.json / v1.1 / v1   旧版本，保留作历史
  index.v1.json              站点索引 index.json
  curator-entry.v1.json      黄页登记文件 curators/<name>.json
LICENSE                      MIT（仅适用于 schema/）
LICENSE-docs                 CC BY 4.0（适用于文档 *.md）
```

**版本：** spec v1.4.5。`SKILL.md` §4.3 列出了各 schema 文件的 hash，请勿修改这些文件的字节。

**授权：** 文档（`*.md`）采用 CC BY 4.0，见 `LICENSE-docs`；`schema/` 下的 JSON Schema 采用 MIT，见 `LICENSE`。

## English

A spec (whitepaper) for agents; **no programs, no template repo** — your own AI writes the code. Tell your agent: *"Read SKILL.md and ACCEPTANCE.md at https://github.com/wangwu-30/daily-skill and build my personal AI daily; ask me what I follow, whom I trust, and what style I like, and do the rest."* It interviews you, builds a personalized daily AI digest in your GitHub account, publishes it (HTML, Markdown, JSON, Atom, llms.txt) and checks itself against `ACCEPTANCE.md`. You only run `gh auth login` and optionally add an LLM API key as a repo secret.

Joining the registry is optional: say "add my digest to https://github.com/wangwu-30/ai-digest-registry" and the agent forks it and opens the PR. Sources are pluggable adapters (§4.2a): add `type: social` + `platform` (e.g. `xiaohongshu`, `jike`) or an `x-<name>` type and one adapter; nothing else changes.

Reference instance: https://www.wangwu.ai/daily/ · Version: spec v1.4.5 · License: docs CC BY 4.0, schemas MIT.
