# 设计交付工程 prompt

design/mockups/ 里 {{PAGE_NAME}} 的静态稿已经定稿,要把它实现到 src/ 里。

请按以下步骤:
1. 读 design/tokens.json 和 design/mockups/{{PAGE_NAME}}.html
2. 在 src/app/ 下建对应路由,用 React + Tailwind 实现
3. 颜色、字号、间距都从 tokens 引用（不要重新写一遍）
4. 实现完跑 eng-review,列出可能的问题
5. 不要主动加我没要求的功能（登录、动画、表单验证等）

注意:
- 用 TypeScript
- 假数据从 data/mock/ 里读
- 写完提示我 git commit
