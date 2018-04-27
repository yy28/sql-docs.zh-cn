---
title: 集成的终端中 SQL 操作 Studio （预览版） |Microsoft 文档
description: 了解有关集成的终端中 SQL 操作 Studio （预览版）。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61d74e7d8818391ca01c45ad8f9a7b2897751712
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="integrated-terminal"></a>集成的终端

在[!INCLUDE[name-sos](../includes/name-sos-short.md)]，你可以打开集成的终端中，最初从你的工作区的根开始。 这会很方便，因为你无需更改现有终端执行快速的命令行任务的状态或切换窗口。

若要打开终端：

* 使用**Ctrl +'** 带有反撇号字符的键盘快捷方式。
* 使用**视图** | **集成终端**菜单命令。
* 从**命令控制板**(**Ctrl + Shift + P**)，使用**视图： 切换集成终端**命令。

![终端](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 你仍可以使用资源管理器打开外部 shell**在命令提示符窗口中打开**命令 (**在终端中打开**在 Mac 或 Linux 上) 如果你希望外部[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

## <a name="managing-multiple-terminals"></a>管理多个终端

可以创建多个终端打开到不同位置，还可以轻松地在它们之间导航。 可以通过点击右上角的加号图标添加终端实例**终端**面板或通过触发**Ctrl + Shift +** 命令。 这将创建另一个项在下拉列表中，可以使用它们之间进行切换。

![多个终端](media/integrated-terminal/terminal-multiple-instances.png)

通过按垃圾桶删除终端实例可以按钮。

> [!TIP]
> 如果广泛使用多个终端，则可以添加键绑定`focusNext`，`focusPrevious`和`kill`命令中所述[密钥绑定部分](#key-bindings)以允许它们仅使用键盘之间导航。

## <a name="configuration"></a>配置

命令行界面使用默认值为`$SHELL`在 Linux 和 macOS，Windows 10 上的 PowerShell 和 cmd.exe 上早期版本的 Windows 上。 可以通过设置手动覆盖这些`terminal.integrated.shell.*`中[设置](settings.md)。 在 Linux 和 macOS 使用上，可以将自变量传递给终端 shell`terminal.integrated.shellArgs.*`设置。

### <a name="windows"></a>Windows

在 Windows 上正确配置您的外壳是一种查找正确的可执行文件并更新设置。 以下是常用的命令行程序可执行文件及其默认位置的列表：

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> 若要用作集成终端，命令行程序可执行文件必须是一个控制台应用程序，以便`stdin/stdout/stderr`可以重定向。

> [!TIP]
> 使用的权限运行集成终端外壳[!INCLUDE[name-sos](../includes/name-sos-short.md)]。 如果你需要使用提升的 （管理员） 或不同的权限运行 shell 命令，你可以使用如平台实用工具`runas.exe`终端中。

### <a name="shell-arguments"></a>命令行程序自变量

启动时，可以将参数传递到命令行界面。

例如，若要启用运行 bash 作为登录 shell (哪些运行`.bash_profile`)，传入`-l`（用双引号） 的自变量：

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>终端显示设置

您可以自定义集成的终端字体和行高度具有下列设置：

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>终端键绑定

**视图： 切换集成终端**命令绑定到**Ctrl +'** 若要快速切换的视图内外的集成终端面板。

以下是用于在集成的终端中快速导航的键盘快捷键：

Key|Command
---|---
**Ctrl +**|显示集成的终端
**Ctrl + Shift +**|创建新的终端
**Ctrl + 向上**|向上滚动
**Ctrl + 向下**|向下滚动
**Ctrl + 向上翻页**|向上滚动一页
**Ctrl + 下翻页**|向下滚动一页
**Ctrl + Home**|滚动到顶部
**Ctrl + End**|滚动到底部
**Ctrl + K**|清除终端

其他终端命令可用，并且可以绑定到你的首选的键盘快捷键。

它们分别是：

* `workbench.action.terminal.focus`： 将重点放终端。 这类似于切换，而是着重而不是隐藏它，终端，如果可见。
* `workbench.action.terminal.focusNext`： 着重终端的下一个实例。
* `workbench.action.terminal.focusPrevious`： 重点介绍在前一个终端实例。
* `workbench.action.terminal.kill`： 删除当前终端实例。
* `workbench.action.terminal.runSelectedText`： 终端实例中运行所选的文本。
* `workbench.action.terminal.runActiveFile`： 终端实例中运行活动的文件。

### <a name="run-selected-text"></a>运行选定的文本

若要使用`runSelectedText`命令，在编辑器中选择文本并运行该命令**终端： 在活动的终端中运行所选文本**通过**命令控制板**(**Ctrl + Shift + P**). 终端尝试运行所选的文本：

![运行选定的文本](media/integrated-terminal/terminal_run_selected.png)

如果在活动编辑器中不选择任何文本，则光标所在的行是在终端中运行。

### <a name="copy--paste"></a>复制和粘贴

用于复制和粘贴键绑定遵循平台标准：

* Linux: **Ctrl + Shift + C**和**Ctrl + Shift + V**
* Mac: **Cmd + C**和**Cmd + V**
* Windows: **Ctrl + C**和**Ctrl + V**

### <a name="find"></a>查找

集成终端具有基本查找功能可与触发**Ctrl + F**。

如果你想**Ctrl + F**若要转到命令行程序而不是启动 Linux 和 Windows 上的查找小组件，你需要删除键绑定如下所示：

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>重命名终端会话

集成的终端会话可以现在重命名使用**终端： 重命名**(`workbench.action.terminal.rename`) 命令。 新名称显示在终端选择下拉列表中。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>强制键绑定来通过终端

集成终端焦点时，多个键绑定将不起作用，因为键击是传递给，供终端本身。 `terminal.integrated.commandsToSkipShell`设置可以用于解决此获取。 它包含其键绑定由 shell 跳过处理和而是由处理命令名称的数组[!INCLUDE[name-sos](../includes/name-sos-short.md)]密钥绑定系统。 默认情况下，这包括所有终端的键绑定，除了选择几个常用键绑定。

