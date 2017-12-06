---
title: "SSMA For Sybase (SybaseToSQL) 中的新 GUI 功能 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d3c60e8c-f0a7-4590-8ece-c68ceaeaea4a
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cb2203520db72867d0aa292aa8d831d185554a4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="new-gui-features-in-ssma-for-sybase-sybasetosql"></a>SSMA For Sybase (SybaseToSQL) 中的新 GUI 功能
本章介绍 SSMA 用户界面的新的功能。  
  
## <a name="layouts"></a>布局  
此功能，可选择两个预定义的窗口布局扩展之一，或创建您自己的布局。 若要访问布局子菜单，在视图菜单上指向布局。 您可以选择一个现有的布局中，添加新的布局或管理布局。  
  
### <a name="add-current-layout"></a>添加当前布局  
若要保存当前窗口布局，在视图菜单中指向布局，然后单击添加当前布局。  
  
### <a name="choose-predefined-layout"></a>选择预定义的布局  
若要选择其中一个预定义的布局，在视图菜单中指向布局，然后单击默认布局或而无需资源管理器。 此外可以使用快捷方式 Ctrl + Alt + 1 或 Ctrl + Alt + 2 的预定义的布局。  
  
### <a name="choose-user-defined-layout"></a>选择用户定义的布局  
若要选择用户定义的布局，在视图菜单中指向布局，，然后单击其中一个的用户定义的布局。 你还可以使用快捷方式为在布局定义。  
  
### <a name="manage-layouts"></a>管理布局  
若要打开管理布局对话框，在视图菜单中指向布局，然后单击管理布局。 在管理布局对话框将对话框左侧查找现有的布局的列表。 你可以选择要更改其设置的布局。 此外可以更改列表中的布局顺序，或删除使用列表顶部的按钮的布局。 在对话框右侧可以更改以下的布局设置：  
  
-   布局名称  
  
-   元数据资源管理器的同步  
  
-   可见性和宽度的源和目标元数据资源管理器  
  
-   源或目标 windows 和其大小的可见性  
  
-   可见性和辅助窗口的高度  
  
## <a name="bookmarks"></a>书签  
此功能可用于在源中设置一个或多个书签或目标代码，快速找到通过使用快捷方式的书签，管理与友好对话框书签。  
  
### <a name="toggle-bookmark"></a>切换书签  
你可以设置/删除书签通过以下方式：  
  
-   在源或目标 SQL 窗口顶部使用按钮切换书签  
  
-   单击 SQL 窗口左侧的灰色区域  
  
-   使用 Ctrl + Shift +&lt;0 到 9&gt;设置带编号的书签  
  
### <a name="bookmark-navigation"></a>书签导航  
你可以通过以下方式逐步书签通过：  
  
-   使用按钮下一个书签，在 SQL 窗口顶部的上一个书签  
  
-   使用 Ctrl +&lt;0 到 9&gt;若要查找带编号的书签  
  
-   使用管理书签对话框的按钮转到或查看源  
  
### <a name="removing-bookmark"></a>删除书签  
可以通过以下方式来删除书签：  
  
-   使用 SQL 窗口顶部清除按钮当前文档中删除所有书签  
  
-   使用管理书签对话框的按钮删除或全部删除  
  
### <a name="manage-bookmarks"></a>管理书签  
若要打开管理书签对话框中的，在编辑菜单上，请单击管理书签。 在对话框中，你将看到现有书签的列表。 可以使用对话框右侧的按钮来管理在书签。  
  
## <a name="object-history"></a>对象历史记录  
GUI 对象历史记录可用于以下优势导航对象时：  
  
-   你可以使用转到后退和前进按钮导航您已经访问的对象  
  
-   当你返回到对象时，你返回到同一选项卡已离开  
  
-   当你返回到对象和选项卡 SQL 时，你返回到相同的光标位置已离开  
  
## <a name="advanced-search-capabilities"></a>使用高级的搜索功能  
使用高级的搜索功能提供的功能强大且灵活的搜索功能，使你查找对象的声明，获取对象的信息、 执行快速搜索，执行高级搜索使用模式等类别中的对象。  
  
### <a name="get-quick-information"></a>快速获取信息  
你可以通过以下方式中的光标位置处的对象上的快速信息：  
  
-   单击 SQL 窗口顶部的按钮快速信息  
  
-   右键单击弹出菜单中选择快速信息  
  
-   按 Ctrl + Shift + 空格键  
  
### <a name="find-declaration"></a>查找声明  
你可以转到以下方式的光标位置处的对象的声明：  
  
-   单击 SQL 窗口顶部的按钮转到声明  
  
-   右键单击弹出菜单中选择转到声明  
  
-   按 f12 键  
  
### <a name="quick-search"></a>快速搜索  
你可以执行快速搜索使用以下功能：  
  
-   你可以开始使用 Ctrl + F 快捷搜索  
  
-   你可以通过使用 F3 重复最后一个搜索转发  
  
-   你可以通过使用 Shift + F3 重复最后一个搜索向后  
  
-   你可以通过使用 Ctrl + F3 查找下一个匹配项的光标位置处的字  
  
-   你可以通过使用 Ctrl + Shift + F3 查找上一个匹配项的光标位置处的字  
  
-   你还可以执行与菜单项的所有这些操作。  
  
### <a name="advanced-search"></a>高级的搜索  
若要打开高级搜索对话框中的，在编辑菜单点查找，然后单击高级搜索。 在对话框中，你将能够查找使用模式的任何对象。 你可以选择对话框顶部搜索区域和对象类别。  
  
