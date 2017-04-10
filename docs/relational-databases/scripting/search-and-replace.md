---
title: "搜索和替换 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "匹配大小写 [SQL Server]"
  - "撤消操作"
  - "搜索 [SQL Server Management Studio]"
  - "替换文本"
  - "快速搜索和替换 [SQL Server Management Studio]"
  - "查询编辑器 [SQL Server Management Studio], 撤消"
  - "查询编辑器 [SQL Server Management Studio], 搜索"
  - "正则表达式 [SQL Server Management Studio]"
  - "查找文本 [SQL Server Management Studio]"
  - "文本 [SQL Server], 搜索和替换操作"
  - "查找 [SQL Server Management Studio]"
  - "找到文本"
  - "查询编辑器 [SQL Server Management Studio], 替换文本"
  - "“查找和替换”对话框"
  - "通配符选项 [SQL Server Management Studio]"
  - "全字匹配 [SQL Server]"
  - "搜索 [SQL Server Management Studio], 替换"
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 搜索和替换
  您可以采用几种不同的方法来查找和替换文本。 在 **“编辑”** 菜单上， **“查找和替换”** 提供了四个选项： **“快速查找”**、 **“快速替换”**、 **“在文件中查找”**或 **“在文件中替换”**。 每个选项均可以打开不同版本的 **“查找和替换”** 对话框。 您还可以通过使用渐进式搜索键盘快捷键在没有对话框的情况下进行搜索。 通过这些技术，您可以控制查找和替换的范围，并选择查看搜索匹配项和替换项的方法。  
  
 搜索和替换文本时应注意以下事项：  
  
-   在 **“查找和替换”** 对话框中设置的选项将影响对文本的搜索。 这些选项包括 **“大小写匹配”**、 **“全字匹配”**、 **“向上搜索”**、 **“搜索隐藏文本”**、 **“通配符”**、 **“正则表达式”**、 **“在所有打开的文档中查找”**以及 **“在当前项目中查找”**。 并非所有版本中的 **“查找和替换”** 对话框均提供了所有选项。  
  
-   **“撤消”** 只适用于在替换操作完成后仍保持打开状态的文档。  
  
-   对跨多个文件的**“全部替换”** 操作执行 **“撤消”** 被视为对所有受影响文件执行的单个大容量操作， 在这种情况下，您不能在某些文件中撤消更改，而在其他文件中保留该更改。  
  
 通常，您无法搜索包含图形视图的项。  
  
## 另请参阅  
 [增量搜索活动文档](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [交互式搜索文档](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用结果列表搜索文档](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [使用通配符搜索文本](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用正则表达式搜索文本](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  