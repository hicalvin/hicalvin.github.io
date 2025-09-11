---
layout: post
title:  生成式AI的崛起26：初试 Vibe Coding 的 10 分钟高效开发体验
date: 2025-09-11 09:10:00 +0800
category: tech
---

> 这是“生成式AI的崛起”系列第 26 篇，记录一次真实的 Vibe Coding（智能代理 + 结对协作节奏）体验：不到 10 分钟，从一个模糊想法，到可运行脚本、功能扩展、项目重构，全程自然语言驱动。

## 背景与诉求

团队里已经累积很多 Wiki / Confluence 内容，这些页面对人类阅读友好，却不利于 LLM 做结构化吸收。参考 `llm.md` 中让知识更 “LLM Ready” 的做法，我想要一个最小工具把这些页面转换为 Markdown：格式统一、易分块、方便后续 embedding + 检索。

初始目标：
1. 抓取通用网页（如 Wikipedia）正文转 Markdown。
2. 支持 Confluence 页面正文（忽略评论 / 侧栏 / 元数据）。
3. 形成可扩展的脚手架，便于后续加并发、分块、元数据注入、差异检测。

## 启动：进入 Vibe Coding 模式

实际操作：
1. 打开一个已有的本地目录（里头有些零散脚本）。
2. 在 GitHub Copilot 中进入 Agent 模式，模型选 Claude Sonnet 4。
3. 给出简单的prompt: "generate a script to convert wiki pages to markdown".

Agent 直接产出了首个 `wiki-to-md.py`，结构清晰。

## 依赖与环境自动修复

首次运行脚本立即报出缺失依赖的错误，我立刻追加第二个 prompt：`help fix the library import issue`。过去遇到这种情况，需要跳到终端或 IDE：手动创建/激活 venv、逐条根据 import 安装依赖、再回到代码验证，思路被多次打断。现在直接交给 Agent，它在同一上下文里解析错误、自动创建虚拟环境、补齐并写入依赖，我只需确认即可继续迭代。
Agent 在同一会话里自动完成环境搭建与修复：
1. 创建并激活虚拟环境 `.venv`
2. 生成 / 合并 `requirements.txt`（仅补缺失依赖，避免重复）
3. 安装所需库并实时输出进度
4. 给出后续运行与验证提示

快速验证：使用示例 URL  
`https://en.wikipedia.org/wiki/Large_language_model`  
顺利生成本地 Markdown 文件（标题层级、链接、强调样式均正确保留），标志最小功能闭环已打通。

## 功能扩展：支持 Confluence

目标：为现有脚本增加 Confluence 页面正文抽取（排除评论、侧栏等噪声）。

使用的新增 prompt：
"please add another method to extract content from confluence page, and only extract page main window content, not including Comments on the page"

Agent 提供的扩展要点：
- requests：获取页面 HTML
- BeautifulSoup：定位主体容器（过滤评论与导航区域）
- html2text：将主体 HTML 转 Markdown（保留标题 / 列表 / 链接）
- urllib.parse：规范化与拼接资源 / 相对链接

验证结果：在内部多页 Confluence 测试中，正文提取准确，未混入评论、侧栏或多余 UI 区块，Markdown 标题层级与链接结构保持良好。

## 项目结构重构

提出的需求：
1. 将 `wiki-to-md.py` 更名为通用入口脚本（支持多站点 / 多提取器）。
2. 将零散演示 / 临时脚本（`hello.py`, `hello.txt`, `deepseek-demo.py`, `example_usage.py`, `check-env.py` 等）归档至 `other/`。
3. 预留扩展目录（如 `converters/`, `pipelines/`），为后续并发、分块、差异检测做空间。

Agent 先给出迁移与命名方案，再按步骤执行（每步前确认），最终结构清晰、语义化、可扩展。

## 体验总结（< 10 分钟）

效率来源：
- 低摩擦表达：仅描述“目标”而非规格细节。
- 持续上下文：无需重复粘贴前序代码或结构。
- 快速闭环：生成 → 运行 → 扩展 → 重构 连续无停顿。

## 当前产出与价值

已具备：
- 支持 Wikipedia / Confluence 抽取为结构化 Markdown 的脚本。
- 初步分层的目录骨架，便于功能沉淀。
- 向后续“知识 → 嵌入 → 检索”链路输送的原始统一格式。

Markdown 后续用途（示例）：
- 向量化：FAISS / Milvus / pgvector
- 分块策略试验：按标题 / 语义 / token
- 注入 front matter：`source_url`, `retrieved_at`, `content_hash`

## 潜在迭代（Backlog）

1. 并发抓取：`asyncio` + `httpx`
2. HTML 去噪规则库：过滤 header / nav / footer / script
3. 分块策略 A/B：结构 vs 语义 vs token 限制
4. 内容差异检测：hash + 变更摘要
5. CLI 增强：`--list --space --output-dir --retry`
6. 质量指标：信息密度 / 重复率 / 平均 token 长度

## 示意性伪代码

```python
class Fetcher:
    def fetch(self, url: str) -> str: ...

class WikiExtractor:
    def extract(self, html: str) -> str: ...

class ConfluenceExtractor:
    def extract(self, html: str) -> str: ...

class Pipeline:
    def run(self, url: str, extractor) -> str:
        html = Fetcher().fetch(url)
        return extractor.extract(html)
```

## 主观感受

Vibe Coding 像持续在线的结对伙伴：我负责方向决策，它负责环境铺设、重复 labor 与结构整理；认知切换次数显著下降，产出密度提升。


