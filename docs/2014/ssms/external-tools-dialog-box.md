---
title: “外部工具”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 60e6ba4d3c9997eaa9052b5d88bf1e2ed625f548
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226637"
---
# <a name="external-tools-dialog-box"></a>外部工具对话框
  使用“外部工具”对话框可以将外部工具（如 SQLCMD 或记事本）添加到“工具”菜单中。 通过添加外部工具，在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境中工作时可以轻松启动其他应用程序。 启动此工具时，可以指定参数及工作目录。 此外，“输出”窗口中可以显示某些工具的输出。 通过“工具”菜单可以打开“外部工具”对话框。  
  
## <a name="options"></a>“常规”  
 **菜单内容**  
 列出当前添加到“工具”菜单上的菜单项标题。 使用“上移”和“下移”箭头可以更改菜单项的显示顺序。 使用“删除”按钮可以从菜单中删除菜单项。  
  
 **上移**  
 将所选工具移动到工具列表（显示在“工具”菜单上）中更靠上的位置。  
  
 **“下移”**  
 将所选工具移动到工具列表（显示在“工具”菜单上）中更靠下的位置。  
  
 **“添加”**  
 清除相应的文本框以便指定新工具。  
  
 **删除**  
 从“菜单内容”列表以及“工具”菜单中删除相应的工具或命令。  
  
 **标题**  
 输入的工具或命令的名称将显示在“工具”菜单的“外部工具”子菜单上。 在工具名称中的一个字母前放置“与”符号 (&)，可以将该字母指定为工具的快捷键。 例如，“&SQLCMD”会在“工具”菜单上显示“SQLCMD”。  
  
 **Command**  
 指定要启动的文件路径。  
  
 **参数**  
 指定在菜单上选择某个工具时传递到该工具的变量。 参数可以指定启动工具或命令时传递给工具或命令的值。 例如，参数值可以指定文件名或目录。 使用箭头按钮可以从预定义的参数列表中进行选择。 您可以添加多个参数。 有关预定义参数及其定义的完整列表，请参阅 [外部工具的参数](menu-help/external-tools.md)。 还可以输入自定义参数（例如，命令行开关），这取决于所使用的命令或工具。  
  
 **使用输出窗口**  
 打开 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 输出窗口显示正在运行命令的输出。 并非所有工具都以在输出窗口中显示的格式显示输出。 有关详细信息，请参阅 [输出窗口](../relational-databases/scripting/transact-sql-debugger-output-window.md)。  
  
 **将输出按 Unicode 处理**  
 将输出解析为 Unicode。  
  
 **初始目录**  
 指定工具的工作目录。 使用箭头按钮可以选择目录。 您可以选择多个目录。  
  
 **提示输入参数**  
 显示“参数”对话框，使用该对话框中可以在每次启动外部工具时输入或编辑参数的值。  
  
 **退出时关闭**  
 在关闭工具时，关闭由该工具打开的窗口。  
  
## <a name="example"></a>示例  
 在“外部工具”对话框中输入以下值将创建标有“DAC”的菜单项，将其选定，便可以使用专用管理员连接打开命令提示符并运行 **sqlcmd** 实用工具。  
  
|Box|ReplTest1|  
|---------|-----------|  
|**标题**|DAC|  
|**Command**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath-md.md)]Tools\Binn\SQLCMD.exe|  
|**参数**|-A|  
  
## <a name="see-also"></a>请参阅  
 [外部工具的参数](menu-help/external-tools.md)   
 [常规用户界面元素](general-user-interface-elements.md)  
  
  
