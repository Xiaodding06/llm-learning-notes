# llm-learning-notes

> 大模型应用开发方向 · 学习笔记仓库（2028届 · 2027 秋招）
> 目标岗位：LLM 应用开发 / Agent 开发 / RAG 工程师

这个仓库是我的学习留痕：**每周的笔记、cheatsheet、项目复盘都推到这里**。
一份连续的 commit 记录，就是简历上最便宜也最难造假的能力证明。

## 为什么是"每周提交"

- 求职执行计划的验收标准之一：**GitHub 提交记录连续 3 个月**
- 每周日 30min 复盘 → 写当周笔记 → commit → push，固定习惯
- 后期所有项目（对话助手 / RAG / Agent / 微调）都在这里立项、迭代

## 仓库结构

```
llm-learning-notes/
├── README.md            # 本文件
├── .gitignore           # 忽略规则（Python 项目通用）
└── notes/
    └── W1/              # 每周一个目录：笔记 + cheatsheet + 练习记录
        ├── README.md            # 本周执行手册（按天拆解）
        ├── git-cheatsheet.md    # git 命令速查 + 练习任务
        ├── linux-cheatsheet.md  # Linux 命令速查 + 练习任务
        ├── environment-notes.md # 本机开发环境盘点与约定
        └── practice-log.md      # 每日练习记录（自己填）
```

## 周笔记索引

| 周 | 主题 | 状态 |
|---|---|---|
| W1 (11.16-11.22) | 环境与版本控制 | 🚧 进行中 |
| W2 (11.23-11.29) | Git 进阶 + Linux + shell 脚本 | ⬜ |
| W3 (11.30-12.06) | FastAPI 入门 | ⬜ |

## Commit 约定

- 消息格式：`类型: 中文描述`，如 `notes: 补充 W1 git 笔记`
- 常用类型：`init` / `notes` / `fix` / `refactor` / `docs`
- 一次 commit 只做一件事；写清楚**为什么**，不只是做了什么
