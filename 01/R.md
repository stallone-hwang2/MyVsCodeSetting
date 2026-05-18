https://tduyng.medium.com/my-vim-setup-in-vscode-c58f8fdcf676


这份 VS Code 配置文件（`settings.json` 和 `keybindings.json`）的核心目的是**将 VS Code 打造为一个深度融合 Vim 操作习惯的高效开发环境**。通过配合 `VSCodeVim` 插件，它不仅让你能在编辑器里用 Vim 键位，还将 Vim 的操作逻辑延伸到了文件树、窗口切换和全局快捷键中。

以下是为你整理的详细功能说明：

---

## 一、 `settings.json`（核心基础设置）

这个文件主要配置了编辑器外观和 **VSCodeVim 插件**的行为。

### 1. 基础体验与 Vim 全局设置

* `"editor.minimap.enabled": false`: 关闭右侧的代码缩略图（Minimap），让代码区域更宽敞。
* `"vim.leader": "<space>"`: **将空格键（Space）设为 Leader 键**。这是你后续大量快捷键的前缀（比如空格 + e 打开侧边栏）。
* `"vim.useSystemClipboard": true`: Vim 的剪切板与系统剪切板同步（用 `y` 复制的内容可以直接用 `Ctrl+V` 粘贴到其他软件）。
* `"vim.easymotion": true` / `"vim.sneak": true` / `"vim.surround": true`: 开启了多个 Vim 极品插件（快速跳转、成对符号修改等）。
* `"vim.smartcase": true`: 搜索时智能大小写（输入全小写时不区分大小写，包含大写字母时严格区分）。

### 2. 模式切换与插入模式快捷键 (`vim.insertModeKeyBindings`)

* **连续快速输入 `jj` 或 `jk**`：直接退出插入模式回到普通模式（等同于按 `Esc`），手不用移到键盘左上角。
* `Ctrl + s`: 在输入模式下直接保存文件（执行 `:w`）。
* `Alt + j` / `Alt + k`: 在输入模式下**直接将当前行上下移动**。

### 3. 普通模式快捷键 (`vim.normalModeKeyBindings`)

* `Tab` / `Shift + Tab`: 快速切换上一个/下一个标签页（Buffer/Editor）。
* `K`: 查看鼠标悬停提示（方法签名、文档等）。
* `g h` / `g l`: 快速跳转到**行首非空字符**（`^`）和**行尾**（`$`）。

### 4. 可视（选择）模式快捷键 (`vim.visualModeKeyBindings`)

* `<` / `>`: 缩进代码。这里做了优化，缩进后**依然保持选中状态**（`g v`），方便连续缩进。
* `g c c` 或 `g c`: 快速注释选中的代码行。

### 5. 快捷键冲突处理 (`vim.handleKeys`)

这里将 `Ctrl + a/f/w/c/v/x/z/y` 的控制权**还给了 VS Code**（设置为 `false`）。这意味着你依然可以使用习惯的 `Ctrl+C` 复制、`Ctrl+V` 粘贴、`Ctrl+F` 搜索和 `Ctrl+W` 关闭窗口，避免了与 Vim 键位的冲突。

---

## 二、 `keybindings.json`（全局快捷键增强）

这个文件进一步将 Vim 逻辑扩展到了全局，尤其是**窗口导航**和**文件浏览器**。

### 1. 视窗导航（原生类似 Vim 体验）

你可以用 `Ctrl` 加上 Vim 的方向键在 VS Code 的各个面板（代码区、侧边栏、终端）之间无缝跳转：

* `Ctrl + h`: 向左切换面板
* `Ctrl + l`: 向向右切换面板
* `Ctrl + k`: 向上切换面板（非输入状态下）
* `Ctrl + j`: 向下切换面板（非输入状态下）

### 2. 强大的 Leader 键（空格开头）组合技

只有在 Vim 的 **Normal 模式**下，按下空格才会触发以下功能：

| 快捷键 | 触发命令 / 功能描述 |
| --- | --- |
| **`Space` + `e**` | **开关侧边栏**。如果在代码区，打开并聚焦到文件树；如果在文件树，关闭侧边栏并回到代码区。 |
| **`Space` + `Space**` | 全局文件搜索（Quick Open，快速打开文件）。 |
| **`Space` + `s` + `g**` | 全局文本搜索（Find in Files）。 |
| **`Space` + `s` + `h**` | **左右分屏**（横向拆分编辑器）。 |
| **`Space` + `s` + `v**` | **上下分屏**（纵向拆分编辑器）。 |
| **`Space` + `b` + `d**` | 关闭当前标签页（Delete Buffer）。 |
| **`Space` + `b` + `o**` | 关闭其他所有标签页（Close Others）。 |
| **`Space` + `c` + `a**` | 触发代码修复建议（Code Action / 灯泡提示）。 |
| **`Space` + `c` + `r**` | 变量/函数**重命名**（Rename）。 |
| **`Space` + `c` + `d**` | 打开底部错误与警告面板（Diagnostics/Problems）。 |
| **`Space` + `g` + `b**` | 打开并聚焦到 Git 版本控制面板（Git Blame/SCM）。 |

### 3. 代码跳转

* `g d`: 跳转到定义（Go to Definition）。
* `g r`: 查看引用（Go to References）。
* `[ d` / `] d`: 在代码的错误/警告之间前后跳转。

### 4. 文件管理器（侧边栏）纯键盘操作

当你的光标聚焦在左侧**文件资源管理器**（Files Explorer）时，你可以像在电脑文件管理器里一样，用单字母快捷键操作文件（必须在非输入状态下）：

* `a`: **新建文件**（Add）
* `r`: **重命名文件**（Rename）
* `d`: **删除文件**（Delete）
* `c`: 复制文件（Copy）
* `x`: 剪切文件（Cut）
* `p`: 粘贴文件（Paste）

---

### 💡 总结

这套配置非常硬核且高效，适合**深度 Vim 用户**或想追求**全键盘操作、丢掉鼠标**的开发者。它借用了类似 SpaceVim 或 Doom Emacs 的双键/三键流（如 `Space b d`），让原本复杂的 VS Code 组合键变得极有规律且容易记忆。