---
title: 集成的终端
titleSuffix: Azure Data Studio
description: 了解有关 Azure Data Studio 中集成终端。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: cfb635287a0baa2d3a9e8f59d9590c278cbf28b2
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010953"
---
# <a name="integrated-terminal"></a>集成的终端

在[!INCLUDE[name-sos](../includes/name-sos-short.md)]，可以打开集成的终端中，最初你的工作区的根目录开始。 这会非常方便，因为你无需切换窗口或更改的现有终端来执行一个快速的命令行任务的状态。

若要打开终端：

* 使用**Ctrl +'** 使用反撇号字符的键盘快捷方式。
* 使用**视图** | **集成终端**菜单命令。
* 从**命令面板**(**Ctrl + Shift + P**)，使用**视图： 切换集成终端**命令。

![终端](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 仍可以使用资源管理器中打开外部 shell**在命令提示符窗口中打开**命令 (**在终端中打开**Mac 或 Linux 上) 如果您想使用外部[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

## <a name="managing-multiple-terminals"></a>管理多个终端

可以创建多个终端打开到不同位置，并在它们之间轻松导航。 可以通过点击右上角的加号图标来添加终端实例**终端**面板，或通过触发**Ctrl + Shift +'** 命令。 这将创建另一个条目在下拉列表中，可以使用它们之间进行切换。

![多个终端](media/integrated-terminal/terminal-multiple-instances.png)

按钮可以通过按回收站删除终端实例。

> [!TIP]
> 如果广泛使用多个终端，则可以添加的键绑定`focusNext`，`focusPrevious`并`kill`命令中所述[键绑定部分](#key-bindings)它们仅使用键盘导航。

## <a name="configuration"></a>配置

使用默认值为 shell `$SHELL` Linux 和 macOS、 Windows 10 上的 PowerShell 和 cmd.exe 在早期版本的 Windows 上。 可以通过设置手动写这些`terminal.integrated.shell.*`中[设置](settings.md)。 Linux 和 macOS 使用，可以将参数传递给终端 shell`terminal.integrated.shellArgs.*`设置。

### <a name="windows"></a>Windows

在 Windows 上正确配置你的 shell 是找到正确的可执行文件并进行更新的设置。 以下是常用的命令行程序可执行文件及其默认位置的列表：

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
> 若要用作集成终端，shell 可执行文件必须是一个控制台应用程序，以便`stdin/stdout/stderr`可以重定向。

> [!TIP]
> 使用的权限运行集成终端 shell [!INCLUDE[name-sos](../includes/name-sos-short.md)]。 如果需要使用提升权限 （管理员） 或不同的权限运行 shell 命令，你可以使用如平台实用程序`runas.exe`终端中。

### <a name="shell-arguments"></a>Shell 参数

启动时，可以将参数传递到 shell。

例如，若要启用作为登录 shell 运行 bash (面授`.bash_profile`)，传入`-l`（用双引号引起来） 的参数：

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>终端的显示设置

使用以下设置，可以自定义集成终端的字体和行高度：

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>终端的键绑定

**视图：切换集成终端**命令绑定到**Ctrl +'** 快速切换入和移出视图集成终端面板。

以下是在集成终端中快速导航的键盘快捷方式：

|Key|Command|  
|---|---|  
|**Ctrl+\`**|显示集成的终端|  
|**Ctrl+Shift+\`**|创建新的终端|  
|**Ctrl+Up**|向上滚动|  
|**Ctrl+Down**|向下滚动|  
|**Ctrl+PageUp**|向上滚动一页|  
|**Ctrl+PageDown**|向下滚动一页|  
|**Ctrl+Home**|滚动到顶部|  
|**Ctrl+End**|滚动到底部|  
|**Ctrl+K**|清除终端|  

其他终端命令可用，并且可以绑定到首选的键盘快捷方式。

它们分别是：

* `workbench.action.terminal.focus`设置用户帐户 ：重点放在终端。 这类似于切换，但主要而不是隐藏它，终端，如果可见。
* `workbench.action.terminal.focusNext`设置用户帐户 ：主要的下一个终端实例。
* `workbench.action.terminal.focusPrevious`设置用户帐户 ：主要的上一个终端实例。
* `workbench.action.terminal.kill`设置用户帐户 ：删除当前终端实例。
* `workbench.action.terminal.runSelectedText`设置用户帐户 ：在终端实例中运行所选的文本。
* `workbench.action.terminal.runActiveFile`设置用户帐户 ：在终端实例中运行活动的文件。

### <a name="run-selected-text"></a>运行选定的文本

若要使用`runSelectedText`命令，在编辑器中选择文本并运行该命令**终端：在活动的终端中运行选定的文本**通过**命令控制板**(**Ctrl + Shift + P**)。 终端会尝试运行所选的文本：

![运行选定的文本](media/integrated-terminal/terminal_run_selected.png)

如果在活动编辑器中不选择任何文本，则是在终端中运行光标所在的行。

### <a name="copy--paste"></a>复制和粘贴

用于复制和粘贴的键盘快捷键遵循平台标准：

* Linux：**Ctrl + Shift + C**和**Ctrl + Shift + V**
* Mac:**Cmd + C**和**Cmd + V**
* Windows:**Ctrl + C**和**Ctrl + V**

### <a name="find"></a>查找

集成终端中具有基本查找功能可与触发**Ctrl + F**。

如果你想**Ctrl + F**若要转到 shell 而不是启动 Linux 和 Windows 上的查找小组件，则需要删除键绑定如下所示：

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>重命名终端会话

集成终端会话可以现在重命名使用**终端：重命名**(`workbench.action.terminal.rename`) 命令。 在终端选择下拉列表中显示的新名称。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>强制通过终端的键绑定

在集成终端焦点时，多个键绑定不会工作，因为键击是传递给和使用的终端本身。 `terminal.integrated.commandsToSkipShell`设置可用于避免这一问题。 它包含其键绑定由 shell 跳过处理并改为处理的命令名称的数组[!INCLUDE[name-sos](../includes/name-sos-short.md)]键绑定系统。 默认情况下，这包括所有终端的键绑定，除了选择几个常用键绑定。

