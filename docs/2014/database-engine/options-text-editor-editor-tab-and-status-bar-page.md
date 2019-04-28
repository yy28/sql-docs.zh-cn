---
title: 选项 (文本编辑器：编辑器选项卡和状态栏页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 241a74861a7f634389324276daf9b03a8590e64d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844267"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>选项 (文本编辑器：编辑器选项卡和状态栏页）
  在 **“编辑器选项卡和状态栏”** 页上，您可以自定义 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 查询编辑器显示的信息。 您可以指定在“查询编辑器”窗口的选项卡和状态栏中显示的信息级别，以及状态栏是显示在编辑器窗口的顶部还是底部。  
  
## <a name="option-settings-by-editor"></a>通过编辑器进行的选项设置  
 编辑器选项卡和状态栏可用于所有 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 编辑器中，但具有不同的功能级别。  
  
 数据库引擎查询编辑器可以连接到服务器组，在这种情况下，它会打开与服务器组中所有实例的连接，并可以同时在每个连接上运行相同查询。 可以使用此对话框指定当连接到多个实例（而非一个实例）时状态栏具有不同的颜色。若要更改多服务器的结果选项，请使用[选项（查询结果/SQL Server/多服务器）](../../2014/database-engine/options-query-results-sql-server-multi-server.md)页。  
  
## <a name="status-bar-content"></a>状态栏内容  
 指定查询编辑器状态栏中显示的信息。  
  
 **显示执行时间**  
 包括脚本执行时间。 其设置包括：  
  
 **无**  
 状态栏不显示任何时间信息。  
  
 **End**  
 当脚本正在运行时，状态栏显示当天的当前时间。 当脚本执行完毕时，屏幕将显示该脚本完成时这一天的时间。  
  
 **已用**  
 状态栏显示脚本一直运行的时间长度。 当脚本执行完毕时，屏幕将显示运行脚本所花的时间。  
  
 **包括数据库名称**  
 包含用于连接的当前数据库的名称。 当首次打开查询编辑器时，这是登录名默认登录的数据库。 之后，可以使用 Transact-SQL USE 语句来更改数据库上下文。  
  
 **包括登录名**  
 包括登录名。  
  
 **包括行计数**  
 包括当前正在执行的脚本已处理过的行的计数。  
  
 **包含服务器名称**  
 包括服务器名称。 对于本地连接，这是实例名称。 对于远程连接，这是远程计算机名称和实例名。  
  
## <a name="status-bar-layout-and-colors"></a>状态栏布局和颜色  
 指定查询编辑器状态栏中项的颜色。  
  
 **组连接**  
 设置查询编辑器具有多个连接时状态栏的颜色。  
  
 **单个服务器连接**  
 设置查询编辑器具有一个连接时状态栏的颜色。  
  
 **状态栏位置**  
 指定状态栏的位置。 其设置包括：  
  
 **Top**  
 状态栏显示在查询编辑器窗口的顶部。  
  
 **底部**  
 状态栏显示在查询编辑器窗口的底部。  
  
## <a name="tab-text"></a>选项卡文本  
 指定查询编辑器窗口顶部的选项卡中显示的文本。 如果文本太长而无法显示，则可以在工具提示中查看完整字符串，当您将鼠标悬停在选项卡上将显示工具提示。  
  
 **包括数据库名称**  
 包含用于连接的当前数据库的名称。 当首次打开查询编辑器时，这是登录名默认登录的数据库。 之后，可以使用 Transact-SQL USE 语句来更改数据库上下文。  
  
 **包含文件名称**  
 包含在其中存储脚本的文件的名称。  
  
 **包括文件夹名称**  
 包含在其中存储脚本文件的文件夹的路径。  
  
 **包括登录名**  
 包括登录名。  
  
 **包含服务器名称**  
 包括服务器名称。 对于本地连接，这是实例名称。 对于远程连接，这是远程计算机名称和实例名。  
  
## <a name="see-also"></a>请参阅  
 [选项&#40;环境：字体和颜色页面&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [查询编辑器中的颜色编码](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
