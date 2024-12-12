# Design docs

# 设计文档

## Commits

## 提交

Each code generation creates a commit. A commit has:

每次代码生成都会创建一个提交。一个提交包含：

- A hash
- A parent hash (null for first version)
- A type (ai_create or ai_edit)
- Inputs (image_url for ai_create, prompt for ai_edit)
- Two variants of code

- 哈希值
- 父哈希值(第一个版本为null)
- 类型(ai_create或ai_edit)
- 输入(ai_create的image_url，ai_edit的prompt)
- 两个代码变体
