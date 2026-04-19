# cc-clean

`cc-clean` 是一个用于清理 Claude 本地状态的小工具，目标是避免“一把梭删掉整个 `~/.claude`”。

它提供：

- 一个受 `codex-session-cloner` 启发的 TUI 界面
- 默认安全预设，不会在未确认时删除旧会话
- 带备份的文件/目录清理流程
- 对 `~/.claude.json:userID` 的定向清理
- 对 `~/.claude/settings.json` 自定义鉴权环境变量的定向清理
- 先生成新标识、再回写旧历史结构化字段的可选流程

## 运行方式

### 方式 1：从源码直接运行

在仓库根目录执行：

```bash
cd /path/to/cc-clean
PYTHONPATH=src python3 -m cc_clean
```

如果你当前就在仓库的 `src/` 目录下，也可以直接：

```bash
cd /path/to/cc-clean/src
python3 -m cc_clean
```

### 方式 2：可编辑安装

```bash
cd /path/to/cc-clean
python3 -m pip install -e .
cc-clean
```

## TUI 与 CLI 的区别

- `python3 -m cc_clean`
- `python3 -m cc_clean tui`

这两个命令会进入交互式 TUI，所以会显示 logo、卡片布局和键盘操作提示。

- `python3 -m cc_clean plan`
- `python3 -m cc_clean clean ...`
- `python3 -m cc_clean remap-history ...`

这些命令是纯文本 CLI 流程，会直接打印结果后退出，不会进入 TUI，也不会显示 logo。

## 常用命令

### 启动 TUI

```bash
PYTHONPATH=src python3 -m cc_clean
```

或者显式使用 `tui` 子命令：

```bash
PYTHONPATH=src python3 -m cc_clean tui
```

### 预览默认安全计划

```bash
PYTHONPATH=src python3 -m cc_clean plan
```

### 执行完整重置并保留备份

```bash
PYTHONPATH=src python3 -m cc_clean clean --preset full --yes
```

### 仅演练，不实际写入

```bash
PYTHONPATH=src python3 -m cc_clean clean --preset safe --dry-run --yes
```

### 先运行 Claude 生成新标识，再回写旧历史

```bash
PYTHONPATH=src python3 -m cc_clean remap-history --run-claude --yes
```
