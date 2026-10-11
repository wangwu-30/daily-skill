# daily-skill：个人 AI 日报 Skill（Personal AI Daily）

[中文](#中文) · [English](#english)

## 中文

这是一份写给 Agent 的规范（白皮书），**不提供任何程序**，也没有模板仓库。代码由你自己的 AI 生成。

**用法：** 把 `SKILL.md` 交给你自己的 Agent。它会先问你 6–10 个问题，了解你的兴趣、信任的人和语言时区，然后在你的 GitHub 账号里搭出一份为你个性化的每日 AI 日报：采集、去重、排序、用自己的话写摘要，再发布成公开网站（HTML、Markdown、JSON、Atom、llms.txt 等，人和 Agent 都能读）。托管可以用 GitHub Actions + Pages，也可以用别的方式。搭好后，Agent 用 `ACCEPTANCE.md` 里的验收标准自检，失败的项自己修。

你最多只需要做两件事：`gh auth login`；可选地把一个 LLM API key 加为仓库 secret，让定时任务自己写摘要。

**参考实例：** https://www.wangwu.ai/daily/

**目录结构：**

```
SKILL.md                     规范正文（给 Agent 读）
ACCEPTANCE.md                验收标准（R 层：公开 URL 可验证；S 层：仓库内自证）
schema/
  digest.v1.3.json           每期 data.json 的当前格式
  digest.v1.2.json           旧版本，保留作历史
  digest.v1.1.json           旧版本，保留作历史
  digest.v1.json             旧版本，保留作历史
  index.v1.json              站点索引 index.json
  curator-entry.v1.json      黄页登记文件 curators/<name>.json
LICENSE                      MIT（仅适用于 schema/）
LICENSE-docs                 CC BY 4.0（适用于文档 *.md）
```

**版本：** spec v1.4.4。`SKILL.md` §4.3 列出了各 schema 文件的 hash，请勿修改这些文件的字节。

**授权：** 文档（`*.md`）采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)，见 `LICENSE-docs`；`schema/` 下的 JSON Schema 采用 MIT，见 `LICENSE`。

## English

This is a spec (a whitepaper) written for agents. **It ships no programs** and no template repo; your own AI writes the code.

**How to use it:** give `SKILL.md` to your own agent. It interviews you with 6–10 short questions (interests, trusted people, language and timezone), then builds a personalized daily AI digest in your GitHub account: it collects, dedupes, ranks, writes summaries in its own words, and publishes a public site (HTML, Markdown, JSON, Atom, llms.txt and more) that both humans and agents can read. Host it with GitHub Actions + Pages or any other way you like. The agent then checks its work against `ACCEPTANCE.md` and fixes what fails.

You do at most two things: run `gh auth login`, and optionally add an LLM API key as a repo secret so the scheduled workflow can write the prose by itself.

**Reference instance:** https://www.wangwu.ai/daily/

**Layout:**

```
SKILL.md                     the spec (for agents)
ACCEPTANCE.md                acceptance criteria (R layer: verifiable from public URLs; S layer: self-attested in the repo)
schema/
  digest.v1.3.json           current format of each issue's data.json
  digest.v1.2.json           older version, kept for history
  digest.v1.1.json           older version, kept for history
  digest.v1.json             older version, kept for history
  index.v1.json              the site index, index.json
  curator-entry.v1.json      registry entry, curators/<name>.json
LICENSE                      MIT (schema/ only)
LICENSE-docs                 CC BY 4.0 (documentation, *.md)
```

**Version:** spec v1.4.4. `SKILL.md` §4.3 lists the hashes of the schema files, so do not change their bytes.

**License:** the documentation (`*.md`) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (see `LICENSE-docs`); the JSON Schemas in `schema/` are licensed under MIT (see `LICENSE`).
