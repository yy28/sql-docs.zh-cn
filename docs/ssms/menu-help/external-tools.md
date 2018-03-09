---
title: "外部工具 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-menu
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.externaltools
helpviewer_keywords: External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc1b7128bfc81f1a30b520e47455e24ec30649a7
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="external-tools"></a>外部工具
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用此对话框可以将外部工具（如 SQL Server 配置管理器或记事本）添加到“工具”菜单。 通过添加外部工具，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中工作的同时，便捷地启动其他应用程序。 启动此工具时，可以指定参数及工作目录。 此外，可以在“输出”窗口中显示某些工具的输出。 通过“工具”菜单可以打开“外部工具”对话框。  
  
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
在“工具”菜单的“外部工具”子菜单上显示的工具或命令的名称。 在工具名称中的一个字母前放置 &amp; 号可以将该字母用作工具的快捷键。 例如，`&Spy++` 将在“工具”菜单上显示为 **Spy++**。  
  
**Command**  
指定要启动的 .exe、.com、.pif、.bat、.cmd 或其他文件的路径。 如果选中“使用输出窗口”复选框，则可以在“输出”窗口中查看 `.bat`、`.com` 和其他文件的输出。  
  
**参数**  
指定在菜单上选择某个工具时传递到该工具的变量。 参数可以指定启动工具或命令时传递给工具或命令的值。 例如，参数值可以指定文件名或目录。 使用“箭头”按钮可以从预定义的参数列表中进行选择。 您可以添加多个参数。 有关预定义参数及其定义的完整列表，请参阅 [外部工具的参数](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)。 根据所用命令或工具的不同，您还可以输入自定义参数（例如，命令提示符开关）。  
  
**初始目录**  
指定工具的工作目录。 使用“箭头”按钮可以选择目录。 您可以选择多个目录。  
  
**使用输出窗口**  
指定是否在“输出”窗口中显示工具的结果。 此选项仅对通常在命令提示符窗口中显示输出的文件（如 .bat 和 .com 文件）可用。 如果启用此选项，则可以在您跟踪工具的进度时简化窗口管理。  
  
**提示输入参数**  
显示“参数”对话框，以便每次启动外部工具时都可以输入或编辑参数的值。  
  
**将输出按 Unicode 处理**  
允许“输出”窗口接受 Unicode。  
  
**退出时关闭**  
在关闭工具时，关闭由该工具打开的窗口。  
  
## <a name="example"></a>示例  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>向“工具”菜单添加 SQL Server 配置管理器  
  
1.  在“工具”菜单上，单击“外部工具”。  
  
2.  在“标题”框中，键入“SQL Server 配置管理器”。  
  
3.  在“命令”框中，键入 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 管理控制台可执行文件的路径，如 **C:\WINNT\system32\mmc.exe**  
  
4.  在“参数”框中，键入 .msc 文件的路径，如 **"C:\WINNT\system32\SQLServerManager.msc"**  
  
> [!NOTE]  
> 查看“开始”菜单上 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 快捷方式的属性，即可确认相应文件在计算机上的位置。  
  
