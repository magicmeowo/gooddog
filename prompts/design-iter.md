# 设计迭代 prompt

我要迭代 {{PAGE_NAME}} 这个页面的设计。

当前问题：{{ISSUE}}

请按以下步骤:
1. 先读 design/references/ 下的灵感参考,找到 1-2 个最相关的
2. 在 design/mockups/{{PAGE_NAME}}.html 里改动（不要新建文件,不要复制一份新的）
3. 改完后跑 ui-ux-pro-max 自检一遍,列出有哪些规则可能没满足
4. 告诉我改了哪几处,理由是什么

注意:
- 一律 HTML + Tailwind 静态稿,不要进 React
- 颜色、字号、间距从 design/tokens.json 引用,不要硬编码
