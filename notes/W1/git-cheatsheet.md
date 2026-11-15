# Git 速查表（W1）

> 目标：不看此表也能完成 增 → 存 → 提 → 推 全流程。

## 0. 核心心智模型：三层 + 远程

```
工作区          暂存区            本地仓库           远程仓库(GitHub)
(你正在改的文件)  (git add 后)      (git commit 后)    (git push 后)
    │── git add ──→│── git commit ─→│─── git push ───→│
    │←─ git checkout/restore ──┐    │←── git pull ────│
    │                          │    │
    └── git diff 看这里         └── git diff --staged 看这里
```

一句话：**add 是"装车"，commit 是"发货入库"，push 是"同步到云端"**。
commit 之前东西只在你硬盘上；push 之后才算"上了 GitHub"，别人（和面试官）才看得见。

## 1. 配置（一次性，本机已完成 ✅）

```bash
git config --global user.name  "Xiaodding06"     # 谁在提交
git config --global user.email "3505581173@qq.com" # 联系方式（GitHub 注册邮箱）
git config --global --list                      # 检查配置
```

## 2. 日常六件套

| 命令 | 作用 | 备注 |
|---|---|---|
| `git status` | 看当前状态 | **用得最多**，迷路就敲它 |
| `git add <file>` / `git add .` | 工作区 → 暂存区 | `.` 是"全部"，新手期可以用 |
| `git commit -m "类型: 描述"` | 暂存区 → 本地仓库 | 消息写清楚**为什么** |
| `git log --oneline --graph` | 查提交历史 | `--oneline` 每条压成一行 |
| `git diff` | 工作区 vs 暂存区 | 改了什么、还没 add 的 |
| `git diff --staged` | 暂存区 vs 最近 commit | add 了但还没 commit 的 |

## 3. 远程操作

```bash
git remote add origin <url>   # 绑定远程仓库（一次性）
git push -u origin main       # 首次推送；-u 记住对应关系，之后只需 git push
git push                      # 日常推送
git pull                      # 拉取远程新内容（多人/多机协作时）
git clone <url>               # 把远程仓库整个下载下来
```

## 4. 高频场景

```bash
git log -p <file>        # 查某文件每次改了什么（代码考古神器）
git show <commit-id>     # 看某次提交的完整改动
git checkout -- <file>   # 丢弃某文件未 add 的改动（危险，不可恢复）
```

**Windows 换行警告**：出现 `warning: LF will be replaced by CRLF` 不用管，是 Windows/Mac/Linux 换行符差异的正常提示，不是错误。

## 5. Commit 消息规范

```
✅ notes: W1 git 练习 1-4 完成，diff 概念已理解
✅ fix: 笔记里管道命令示例参数写错
❌ 更新              ← 更新了什么？
❌ 1111             ← 三个月后自己都看不懂
```

---

## 练习任务（做完把感受记进 practice-log.md）

1. 在仓库里新建 `notes/W1/test.txt`，写入一行文字，用 `git status` 观察它出现在哪一栏，再 `git add` 后看变化。
2. `git commit` 提交它，然后 `git log --oneline` 找到这次提交。
3. 修改 test.txt 再加一行，分别执行 `git diff` 和 `git diff --staged`，对比两者输出差异，用自己的话写下区别（这就是三层模型的考点）。
4. 把 test.txt 删掉，用 `git checkout -- test.txt` 恢复它，体会"没 commit 的改动 = 随时会丢"。
5. 故意把 README.md 改坏（随便删几行），`git diff README.md` 看删除了什么，再用 checkout 恢复。
6. `git log -p README.md` 看这个文件的全部历史改动。
7. push 一次后，去 GitHub 网页上找到这次 commit，点进去看 diff——确认"本地 diff 和网页 diff 是同一个东西"。
