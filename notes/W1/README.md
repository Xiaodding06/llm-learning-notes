# W1 执行手册：环境与版本控制（11.16 - 11.22）

> 本周目标：把"写代码 → 提交 → 推送"变成肌肉记忆，产出这个仓库本身。
> 每天投入 1-1.5h，周末半天。**做完当天的任务就 commit 一次，别攒。**

## 本周大盘

| 任务 | 落点 | 已由布丁代劳的部分 |
|---|---|---|
| GitHub 账号整理 | Day 1 | —（需要你自己登录） |
| git 基本流程 | Day 2-3 | 仓库骨架 + 首次 commit 已完成，照着流程复盘 |
| Linux 常用命令 | Day 4-5 | cheatsheet 已备好，Git Bash 即可开练 |
| 本地环境整理 | Day 6 | 现状盘点已写进 environment-notes.md |
| 周复盘 | Day 7 | practice-log.md 模板已备好 |

## 按天拆解

### Day 1（周一 11.16）：GitHub 账号整理 · ~45min
- [ ] 登录 GitHub（账号应为 **Xiaodding06**，与本机 git 全局配置一致，push 时免疑惑）
- [ ] 完善个人主页：头像（不用真人照）、一句话 bio（如"LLM 应用开发学习中"）、院校/方向可写可不写
- [ ] 练习浏览：搜索 `fastapi`、`langchain`、`llama-index`，各 star 一个——以后这就是你的技术雷达
- [ ] 回来在本文件勾掉这一行，今晚第一次 commit（见 Day 2 流程，提前跑通一遍也行）

### Day 2（周二 11.17）：git 三板斧 add / commit / status · ~1h
- [ ] 打开 Git Bash（开始菜单搜 "Git Bash"），`cd /d/llm-learning-notes`
- [ ] 依次执行并观察输出：`git status` → `git log --oneline` → 改动 practice-log.md 里今天的记录 → `git status`（看文件变红）→ `git add` → `git status`（变绿）→ `git commit`
- [ ] 完成 git-cheatsheet.md 底部的**练习 1-4**，把答案/截图记进 practice-log.md
- [ ] 理解核心：**工作区 → 暂存区 → 本地仓库** 三层模型（cheatsheet 顶部有图解说）

### Day 3（周三 11.18）：接上 GitHub + log / diff · ~1h
- [ ] GitHub 网页上新建仓库 `llm-learning-notes`，**不要**勾选 README/.gitignore（本地已有）
- [ ] 本地执行：
  ```bash
  git remote add origin https://github.com/Xiaodding06/llm-learning-notes.git
  git push -u origin main
  ```
  会弹出 GitHub 登录窗口（Git Credential Manager），浏览器授权一次即可
- [ ] 刷新网页确认代码上去了——**这一刻起你的提交记录开始计时**
- [ ] 完成 cheatsheet **练习 5-7**：故意制造一次改动，用 `git diff` 看差异，再 `git log -p` 回看历史

### Day 4（周四 11.19）：Linux 命令上半场 · ~1h
- [ ] 全程在 Git Bash 里练（它就是个精简 Linux 环境）
- [ ] 完成 linux-cheatsheet.md **练习 1-6**：cd / ls / cat / grep / 管道 / 重定向
- [ ] 重点体会管道：`ls -la | grep notes` 这种"小命令拼大功能"的思想，后面写 shell 脚本全靠它

### Day 5（周五 11.20）：Linux 下半场：权限 + WSL（可选）· ~1h
- [ ] 理解 rwx 权限模型（cheatsheet 有图解），Git Bash 上 `ls -l` 看权限位
- [ ] **可选**：管理员 PowerShell 执行 `wsl --install` 装 Ubuntu（装不装不影响验收，W2 要 ssh 服务器，到时候必须练）。WSL 装好后 `wsl` 进入，把练习 1-6 原样再跑一遍
- [ ] 不装 WSL 就把时间省下来，多做几道 grep 管道组合题

### Day 6（周六 11.21，半天）：本地环境整理 · ~1.5h
> 修订（11.19）：原计划拿旧课程项目 pythonProject 练手，但它与大模型求职主线无关。
> 改为**从零新建** `D:\llm-app-lab`，作为 W3 起 FastAPI / RAG / Agent 代码的落点。

- [ ] 读 environment-notes.md，确认"系统 Python 当裸机工具、项目一律 venv"的约定
- [ ] 新建独立项目 + 独立 venv（**不要用 pythonProject 的 venv**）：
  ```bash
  mkdir -p /d/llm-app-lab
  "C:/Users/小丁/AppData/Local/Programs/Python/Python39/python.exe" -m venv /d/llm-app-lab/.venv
  ```
- [ ] 装两个 LLM 应用真正会用到的包，再生成 requirements.txt：
  ```bash
  /d/llm-app-lab/.venv/Scripts/python.exe -m pip install requests python-dotenv -i https://pypi.tuna.tsinghua.edu.cn/simple
  /d/llm-app-lab/.venv/Scripts/python.exe -m pip freeze > /d/llm-app-lab/requirements.txt
  cat /d/llm-app-lab/requirements.txt | head -20
  ```
- [ ] 用 `>` / `>>` 写 .gitignore：`.venv/`、`.idea/`、`__pycache__/`、`.env`、`*.pth`
- [ ] 写一份 5 行 README：这个项目做什么、怎么还原环境（`pip install -r requirements.txt`）
- [ ] **可选**：把它变成第二个 repo 推上 GitHub（W3 的 FastAPI 代码就往这里提交）
- [ ] 说清楚：`D:\学习资料\pythonProject` 是课程作业，与求职主线无关，不动它

### Day 7（周日 11.22，30min）：复盘 + 收尾
- [ ] 填完 practice-log.md 本周全部记录
- [ ] 检查验收清单（下方），全绿即 W1 达成
- [ ] commit + push，写周报式 commit：`notes: W1 复盘——环境与版本控制完成`
- [ ] 预习 W2：分支 / merge / 冲突（下周主菜）

## W1 验收清单
- [ ] GitHub 上有 llm-learning-notes 仓库，且至少 5 个 commit
- [ ] 能不看笔记说出 add/commit/push 各自把代码送到了哪一层
- [ ] 能用 grep + 管道在一个文件里筛出想要的内容
- [ ] 能解释 `ls -l` 输出里每个字段的意思
- [ ] 说清楚自己的机器上"哪个 Python 服务于哪个项目"
