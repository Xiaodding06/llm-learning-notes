# 本机开发环境盘点与约定（2026-11-15 由布丁核查）

## 一、现状盘点（已核实）

| 组件 | 状态 | 说明 |
|---|---|---|
| Git | ✅ 2.55.0 | 全局配置已设：Xiaodding06 / 3505581173@qq.com |
| Git Credential Manager | ✅ 2.9.0 | push 到 GitHub 会弹浏览器授权，**无需配 SSH key** |
| 系统 Python | 3.9.2 | `C:\Users\小丁\AppData\Local\Programs\Python\Python39\`，已装 torch(cpu)/numpy/matplotlib/python-docx |
| PyCharm 项目 venv | ✅ | `D:\学习资料\pythonProject\.venv`（Python 3.9），已装 numpy/matplotlib/torch 2.8.0+cpu/torchvision |
| conda | ❌ 未安装 | 暂无必要，见下方"决策" |
| WSL | 未确认 | 沙箱里检测被拦，Day 5 自行在管理员 PowerShell 跑 `wsl --install` |
| 显卡 | RTX 4050 Laptop | 驱动 572.70 / CUDA 12.8；当前 torch 是 CPU 版 |

## 二、约定（从今天起执行）

1. **系统 Python = 裸机工具**：只拿来跑脚本、装轻量包（requests、jupyter 之类）。
   任何正经项目一律 venv 隔离，避免"装包打架"。
2. **一个项目一个 venv**：PyCharm 新建项目时默认自带 `.venv`，保持这个习惯即可。
   手动建的话：
   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1    # 激活后 pip 装的包只进这个项目
   ```
3. **每个项目根目录维护 `requirements.txt`**：
   ```powershell
   .\.venv\Scripts\python.exe -m pip freeze > requirements.txt
   ```
   别人（和三个月后的你）靠它一键还原环境：`pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple`
4. **装包统一走清华源**（快一个数量级）：`-i https://pypi.tuna.tsinghua.edu.cn/simple`

## 三、为什么现在不装 conda

- venv 已覆盖当前全部需求（每个项目独立、干净、PyCharm 原生支持）
- conda 的真正价值在**多 Python 版本共存 + CUDA 相关包管理**，等 W23 做微调、需要 PyTorch GPU 版或多版本切换时再装 miniconda 也不迟
- 少一层工具 = 少一层坑。先把手头工具用熟。

## 四、本机已知坑（记录在案，遇到不慌）

- **pip 装大包退出码报错 ≠ 安装失败**：沙箱的批量删除保护会拦 pip 清理临时文件，常见 `SystemExit: 1` / safe-delete 报错，但包其实装好了。判定方法：直接 `python -c "import xxx"` 验证，不要凭退出码重装。
- **PyCharm 报 ModuleNotFoundError 时**，装包要指定项目 venv 的 pip（系统 Python 装了不算数）：
  `& "D:\学习资料\pythonProject\.venv\Scripts\python.exe" -m pip install <pkg> -i https://pypi.tuna.tsinghua.edu.cn/simple`
- **matplotlib 中文乱码**：`plt.rcParams["font.sans-serif"] = ["Microsoft YaHei"]`
- **torch 是 CPU 版**（`torch.cuda.is_available() == False`）：现阶段够用，W8 之后跑 Transformer 小实验、W23 微调时再装 GPU 版或转 AutoDL 租卡。
- **脚本命名**：别用 `inspect.py` 等会遮蔽标准库模块名的文件名。

## 五、中期待办（先记下，不着急）

- [ ] W5 前后：注册 DeepSeek / 通义 API key
- [ ] W23 前后：PyTorch GPU 版 or miniconda or AutoDL，三选一
- [ ] 把 pythonProject 推上 GitHub（Day 6 可选任务，趁热做掉）
