# W1 复习卡（忘了就翻这里）

> **不用从头读。** 按「我现在卡在哪」跳到对应一节即可。
> 覆盖：Git 三层模型 / 撤销恢复 / diff / Linux 命令 / 权限 rwx / 环境归属 / 报错速查。
> 最后两节（第 8、9 节）是重点：还漏风的 3 个钉子、以及这周你已经拿下的东西。

---

## 0. 一页速查（最高频）

| 命令 | 人话 | 送到哪一层 |
|---|---|---|
| `git status` | 现在啥情况（迷路专用） | — |
| `git add 文件名` | 把改动放进「待存清单」 | 工作区 → 暂存区 |
| `git status` | 看完 add 再确认一次 | — |
| `git commit -m "类型: 干了什么"` | 拍一张快照存档 | 暂存区 → 本地仓库 |
| `git push` | 把快照同步上云 | 本地仓库 → GitHub |
| `git log --oneline` | 列出所有历史快照 | — |

**红绿口诀**：`红 → add → 绿 → commit → clean → push`
红色 = 改动没 add，停在**工作区**；绿色 = 已 add，停在**暂存区**；`working tree clean` = 全存完了。

**commit 消息**是写给三个月后的自己看的，格式 `类型: 干了什么、为什么`：
`✅ notes: 填写练习日志 Day 3` ／ `❌ 更新` ／ `❌ 1111`
常用类型：`notes` 笔记、`test` 试验、`fix` 修错、`docs` 文档、`init` 初始化。

---

## 1. Git 三层模型（所有 git 问题的根）

```
工作区          暂存区            本地仓库（= 档案册）     远程仓库 (GitHub)
(你正在改的文件)  (git add 后)       (git commit 后)        (git push 后)
   │── git add ──→│── git commit ─→│─── git push ───→│
```

- **四个名字其实是三个地方**：本地仓库 = 档案册，是同一个东西的两种叫法，都在 `.git/` 文件夹里。
- `HEAD` 不是第四格，是贴在档案册上的**书签**，永远指向最新那张快照。
- **同一个文件可以同时有三个不同版本**（工作区 / 暂存区 / 快照），互不覆盖，所以 diff 才有意义。
- **你施工，git 拍照**：真正改动文件内容的只有你（notepad / echo / rm）。git 全程只登记、拍照、对比、上传，**从不碰文件内容**。
- `git add` ≠ 上传；本地三格之间只是「登记 / 存档」，只有 `push` 是真上传。

**状态语翻译**

| 看到 | 意思 |
|---|---|
| `nothing to commit, working tree clean` | 该存的都存了 |
| `Your branch is up to date with 'origin/main'` | 本地和云端完全一致 |
| `Your branch is ahead of 'origin/main' by 1 commit` | 本地多 1 条，**该 push 了** |

---

## 2. 撤销与恢复（最容易错，重点看）

| 症状 | 用哪条 | 从哪恢复 |
|---|---|---|
| 改坏了，**还没 add** | `git checkout -- 文件名` | 暂存区 → 工作区 |
| `git rm` 删掉了 | `git checkout HEAD -- 文件名` | 最近快照 → 工作区 + 暂存区 |
| 从没 commit 过就被删了 | **救不回来** | 快照里根本没这张照片 |

- `git rm` = 删工作区文件 **+ 把暂存区里这份也划掉**，所以 `checkout --`（照暂存区恢复）会报「不认识这个文件」。
- **能恢复的唯一前提 = commit 过。没 commit 的东西，在 git 眼里不算存在过。**
- `git rm` 对「add 过但没 commit」的文件会主动拦你（保护最后一道门），加 `-f` 强删后就真没了。
- `rm` 只删工作区，`git rm` 连暂存区一起清空——两者不是一回事。

**断电丢不丢**：`add` 过的改动已存进 `.git`（断电**不丢**）；**没 add** 的纯工作区改动才可能丢。→ 勤 commit。

---

## 3. diff 两兄弟

| 命令 | 比较哪两样 | 一句话 |
|---|---|---|
| `git diff` | 工作区 **vs** 暂存区 | 装车前后差多少 |
| `git diff --staged` | 暂存区 **vs** 最近快照 | 这次结账要买多少 |

- 输出里 `--- a/` 是旧版、`+++ b/` 是新版，`-` 删掉的、`+` 新增的。
- **`git diff` 空白 = 两个区一模一样，不是出错，也不是「没 add」**；最常见的原因恰恰是**已经 add 了**。
- add 之后两个命令输出会「互换」：`git diff` 变空白、`--staged` 有内容。这不是失灵，是三格的版本关系变了。

---

## 4. Linux 命令

| 命令 | 作用 |
|---|---|
| `pwd` / `cd 目录` | 我在哪 / 去哪（`cd ..` 上级、`cd ~` 家目录） |
| `ls -la` | 列文件；`-l` 详细、`-a` **连隐藏文件一起显示**（`.git/` 靠它才看得见） |
| `cat 文件` | 打印文件全文 |
| `head -20` / `tail -20` | 前 20 行 / 后 20 行 |
| `grep "词" 文件` | 把含这个词的**整行**拎出来：`-n` 行号、`-i` 忽略大小写、`-r` 递归、`-c` 计数 |
| `grep -c ""` | 数输出有几行 |
| `history` | 列出敲过的命令（复习神器） |

**输出格式**：`grep -n` 是 `行号:原文`；`grep -rn` 是 `路径:行号:原文`。空白 = 0 个匹配，不是没执行。

### 管道与重定向（Day 4 灵魂）

```bash
命令A | 命令B        # A 的输出喂给 B 当输入 —— 给「命令」
命令 > 文件          # 输出【覆盖】写进文件 —— 给「文件」
命令 >> 文件         # 输出【追加】到文件末尾
```

- **管道给命令，重定向给文件。**
- `echo "一行" > demo.txt` 敲完屏幕一片安静 = 成功了，输出被 `>` 改道搬进文件了，用 `cat demo.txt` 取出来看。
- 管道可以串好几级：`cat train.log | grep loss | wc -l`
- **尾部接的程序决定输出**：`head -20` 打印前 20 行；`wc -l` 输出**一个行数数字**（比如 `37`），不是那些行。
- 以后盯训练：`tail -f train.log | grep loss`，同款套路。

---

## 5. 权限 rwx

`-rw-r--r--` 这串**一共 10 位 = 1 位类型 + 9 位权限**：

```
-   rw-   r--   r--
↑    ↑     ↑     ↑
类型  u     g     o        u=所有者 g=同组 o=其他人
```
`-` 普通文件 / `d` 目录 / `l` 软链接。9 位 = 3 组 × 3 位，每组顺序**永远固定 r→w→x**，缺的写 `-` 占位。

**数字换算**：`r=4 w=2 x=1` 相加。644 = `rw-r--r--`，755 = `rwxr-xr-x`，600 = `rw-------`，750 = `rwxr-x---`。

**同一个字母，对文件和目录含义不同（最易混）**

| | 文件 | 目录 |
|---|---|---|
| `r` | 看内容 | **灯**：`ls` 列得出文件名 |
| `w` | 改内容 | 新建 / 删除 / 改名文件 |
| `x` | 当程序跑 | **门**：`cd` 进得去 |

- 目录 `r--` = **有灯没门**：能 `ls`，**不能 cd**；`--x` = 有门没灯：能进，列不出。所以目录几乎都是 755（带 x）。
- `644` 的脚本敲 `./script.sh` → `Permission denied`（三组都没有 x），要先 `chmod +x script.sh` 变 755。**W2 写 shell 脚本第一道手续**。
- `600` 用于 ssh 私钥 / `.env` 里的 API key，是**硬性要求**：设成 644 会报 `Permissions are too open`，ssh 直接拒绝连接。`777` 危险，别用。
- `chmod 644 文件` 数字法；`chmod +x 文件` 符号法；`u/g/o` 对应三组。
- Windows / Git Bash 权限是**模拟**的，练读和算即可，真实语义等装 WSL 后验证。

---

## 6. 环境与项目归属

| 项目 | 路径 | 干什么 |
|---|---|---|
| 课程作业 | `D:\学习资料\pythonProject` | MNIST，**不动它** |
| 笔记仓库 | `D:\llm-learning-notes` | 学习记录（Git Bash 里 `/d/llm-learning-notes`） |
| 求职主线 | `D:\llm-app-lab` | W3 起 FastAPI / RAG / Agent 代码 |
| Linux 练习场 | `D:\学习资料\linux-lab` | 乱敲命令用，在 git 仓库外（提示符无 `(main)`） |

- **系统 Python 当裸机工具，正经项目一律一个项目一个 venv**，避免装包打架。
- `requirements.txt` = 这套 venv 的完整配方，靠 `pip freeze > requirements.txt` 生成，别人用 `pip install -r requirements.txt` 一键还原。**它要进 git，`.venv/` 不进**（几百 MB 且每台机器可重装）。
- `.gitignore` 负责挡住不该进 git 的东西（`.venv/`、`.env`、`*.pth`）；`git check-ignore -v .venv/` 可以问 git「凭啥不理它」。
- 装包走清华源：`-i https://pypi.tuna.tsinghua.edu.cn/simple`。PyCharm 报模块找不到时，要用**该项目自己 venv 的 pip** 装，系统 Python 装了不算。
- **git 仓库是自包含的**：整个文件夹搬家，`.git` 跟着走，历史、快照、origin 全在。远程 URL 只是个字符串，跟仓库在硬盘哪个角落无关。
- 仓库里 `ls -l` 看不到 `.git/` 是因为它是点开头的隐藏文件，`-a` 才能看见。

---

## 7. 报错速查（这周真踩过的）

| 报错 / 现象 | 意思 | 怎么办 |
|---|---|---|
| `command not found` | 把中文动作描述当命令敲了 | 「改动文件」要用 `notepad 文件`，终端只认命令 |
| `No such file or directory` | `cd` 的路径不存在 | 逐段检查路径拼写 |
| `did not match any files` | 文件名 / 路径拼错 | **`git add notes/W1/pra` 然后按 Tab 补全** |
| `no changes added to commit` | **忘了 add**（空购物车结不了账） | 补 `git add 文件名` 再 commit |
| `did not match any file(s) known to git` | `git rm` 后用 `checkout --` | 换 `git checkout HEAD -- 文件名` |
| `warning: LF will be replaced by CRLF` | Windows 换行符差异 | **无害，忽略** |
| `git push` 报 `Connection was reset` / `schannel` | GitHub 直连瞬时抽风 | **隔一会儿重试 2-3 次**；commit 早在本地，push 失败永不丢数据 |
| 终端出现 `>` 不动了 | 命令末尾多打了 `\`，bash 在等续行 | `Ctrl+C` 取消重来 |
| `Permission denied` | 文件没有 x 位 | `chmod +x` |
| `git diff` 一片空白 | 两区一致 | 不是报错，见第 3 节 |

---

## 8. 还漏风的 3 个钉子（11.24 抽测后，复习优先级最高）

1. **`git checkout HEAD -- 文件名` 要写全**：`HEAD` 全大写、前后空格、`--` 后面必须跟文件名。写成 `--head` 是错的，这题已经错 3 次。配套记住另一条：改坏没 add 用 `git checkout -- 文件名`。
2. **`git diff` 空白 = 工作区与暂存区一致**（通常是已经 add 了），**不是「文件没 add」**。反过来，没 add 但改过，diff 反而有输出。
3. **add 后断电不丢，没 add 才可能丢**。commit 是唯一的保险箱。

> 诊断：讲顺序、讲概念全对；说「精确命令 / 具体后果」就丢分。复习时别只看懂，要**能默写命令**。

---

## 9. 这周已经拿下的（不用再学，保持住）

- ✅ 完整工作流：改 → add → commit → push，独立跑通很多次
- ✅ `git status` 红 / 绿含义、`git log --oneline`、commit 消息规范
- ✅ 三层模型、HEAD 是什么、git 从不改文件内容
- ✅ `git diff` 与 `--staged` 的两对比较、add 后的「互换」
- ✅ 目录 `r--` 有灯没门（不能 cd）、`644` 脚本要 `chmod +x`、`600` 是 ssh 硬性要求
- ✅ `>` 覆盖 / `>>` 追加、管道末尾接 `wc -l` 输出数字
- ✅ 10 位权限拆解、644 / 755 / 600 / 750 换算
- ✅ 三个项目各归各、venv 纪律、requirements.txt、`.gitignore` 挡住 `.venv/`
- ✅ 仓库搬家后 `.git` 自包含；push 网络故障自己重试成功

**产出**：2 个 GitHub 仓库、11 条提交，绿格子从 11.16 开始计时。
