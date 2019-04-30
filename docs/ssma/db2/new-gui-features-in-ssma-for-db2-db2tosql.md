---
title: SSMA for DB2 中的新增 GUI 功能 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a8ed33e9-185a-492d-a4cf-2fded1aa5c70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b15759f9cee25c214ba67c09590f46093d41f22f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280899"
---
# <a name="new-gui-features-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 中的新增 GUI 功能 (DB2ToSQL)
本章节介绍了 SSMA 用户界面的新功能。  
  
## <a name="layouts"></a>布局  
此功能，可选择一个预定义的两个窗口排列或创建自己的布局。 若要访问布局子菜单，请在视图菜单上指向布局。 您可以选择一个现有的布局，添加新的布局或管理布局。  
  
### <a name="add-current-layout"></a>添加当前布局  
若要保存当前窗口布局，在视图菜单中指向布局，然后单击添加当前布局。  
  
### <a name="choose-predefined-layout"></a>选择预定义的布局  
若要选择一个预定义的布局，在视图菜单中指向布局，然后单击默认布局或没有资源管理器。 此外可以使用快捷方式 Ctrl + Alt + 1 或 Ctrl + Alt + 2 的预定义的布局。  
  
### <a name="choose-user-defined-layout"></a>选择用户定义的布局  
若要选择用户定义的布局，在视图菜单中指向布局，，然后单击其中一个用户定义的布局。 此外可以使用快捷方式定义的布局。  
  
### <a name="manage-layouts"></a>管理布局  
若要打开管理布局对话框，在视图菜单中指向布局，然后单击管理布局。 在管理布局对话框将在对话框的左侧找到现有布局的列表。 那里您可以选择要更改其设置的布局。 此外可以更改布局列表中的顺序，或删除使用列表顶部的按钮的布局。 在对话框右侧可以更改以下布局设置：  
  
-   布局名称  
  
-   元数据资源管理器的同步  
  
-   可见性和宽度的源和目标元数据资源管理器  
  
-   源或目标 windows 和其大小的可见性  
  
-   可见性和辅助窗口的高度  
  
## <a name="bookmarks"></a>书签  
此功能允许你在源中设置一个或多个书签或目标代码，快速找到一个书签，通过使用快捷方式、 管理与友好对话框书签。  
  
### <a name="toggle-bookmark"></a>切换书签  
您可以设置/删除一个书签，按以下方式：  
  
-   使用源或目标 SQL 窗口的顶部的按钮切换书签  
  
-   单击 SQL 窗口左侧的灰色区域  
  
-   使用 Ctrl + Shift +&lt;0 到 9&gt;设置带编号的书签  
  
### <a name="bookmark-navigation"></a>书签导航  
您可以放心离开书签在通过以下方式：  
  
-   使用按钮下一个书签，SQL 窗口顶部的上一个书签  
  
-   使用 Ctrl +&lt;0 到 9&gt;若要查找带编号的书签  
  
-   使用管理书签对话框中的按钮转到或查看源  
  
### <a name="removing-bookmark"></a>删除书签  
可以按以下方式来删除书签：  
  
-   使用 SQL 窗口顶部的清除按钮当前文档中删除所有书签  
  
-   使用在管理书签对话框删除或全部删除按钮  
  
### <a name="manage-bookmarks"></a>管理书签  
若要打开管理书签对话框中的，在编辑菜单上，请单击管理书签。 在对话框中，您将看到一个现有书签列表。 可以使用对话框右侧的按钮来管理书签。  
  
## <a name="object-history"></a>对象历史记录  
GUI 对象历史记录，以下优点导航对象时：  
  
-   可以使用转到后退和前进按钮来导航您已经访问的对象  
  
-   当你回到对象时，备份到同一选项卡上还剩  
  
-   当您返回到对象和选项卡是 SQL 时，备份到同一还剩的光标位置  
  
## <a name="advanced-search-capabilities"></a>高级的搜索功能  
高级的搜索功能提供功能强大且灵活的搜索功能，让您查找对象的声明、 获取对象的信息、 执行快速搜索、 执行高级搜索使用模式等类别中的对象。  
  
### <a name="get-quick-information"></a>快速获取信息  
就可以通过以下方式中的光标位置处的对象上的快速信息：  
  
-   单击 SQL 窗口顶部的按钮快速信息  
  
-   右键单击弹出菜单中选择快速信息  
  
-   按 Ctrl + Shift + 空格键  
  
### <a name="find-declaration"></a>查找声明  
你可以转到以下方面的光标位置处的对象的声明：  
  
-   单击 SQL 窗口顶部的按钮转到声明  
  
-   右键单击弹出菜单中选择转到声明  
  
-   按 f12 键  
  
### <a name="quick-search"></a>快速搜索  
您可以执行快速搜索使用以下功能：  
  
-   你可以开始搜索使用快捷方式 Ctrl + F  
  
-   您可以通过使用 F3 重复最后一个搜索前滚  
  
-   您可以通过使用 Shift + F3 重复最后一个搜索向后  
  
-   你可以通过使用 Ctrl + F3 查找光标位置处的单词的下一个匹配项  
  
-   你可以通过使用 Ctrl + Shift + F3 查找光标位置处的单词的上一个匹配项  
  
-   此外可以执行所有这些操作与菜单项。  
  
### <a name="advanced-search"></a>高级的搜索  
若要打开高级搜索对话框上编辑菜单点查找，然后单击高级搜索。 在对话框中您将能够找到使用模式的任何对象。 你可以选择在对话框顶部搜索区域和对象的类别。  
  
