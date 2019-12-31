---
title: 搜索和替换
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 631b6864529e903516857f68ea421365c144afef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243304"
---
# <a name="search-and-replace"></a>搜索和替换
  您可以采用几种不同的方法来查找和替换文本。 在 **“编辑”** 菜单上， **“查找和替换”** 提供了四个选项： **“快速查找”**、 **“快速替换”**、 **“在文件中查找”** 或 **“在文件中替换”**。 每个选项均可以打开不同版本的 **“查找和替换”** 对话框。 您还可以通过使用渐进式搜索键盘快捷键在没有对话框的情况下进行搜索。 通过这些技术，您可以控制查找和替换的范围，并选择查看搜索匹配项和替换项的方法。  
  
 搜索和替换文本时应注意以下事项：  
  
-   在 **“查找和替换”** 对话框中设置的选项将影响对文本的搜索。 这些选项包括 **“大小写匹配”**、 **“全字匹配”**、 **“向上搜索”**、 **“搜索隐藏文本”**、 **“通配符”**、 **“正则表达式”**、 **“在所有打开的文档中查找”** 以及 **“在当前项目中查找”**。 并非所有版本中的 **“查找和替换”** 对话框均提供了所有选项。  
  
-   **Undo**仅适用于替换操作后保持打开状态的文档。  
  
-   对跨多个文件的 "全部**替换**" 操作执行 "**撤消**" 被视为对所有受影响文件执行单个大容量操作。 在这种情况下，您不能在某些文件中撤消更改，而在其他文件中保留该更改。  
  
 通常，您无法搜索包含图形视图的项。  
  
## <a name="see-also"></a>另请参阅  
 [增量搜索活动文档](search-an-active-document-incrementally.md)   
 [交互式搜索文档](search-documents-interactively.md)   
 [使用结果列表搜索文档](search-documents-using-results-lists.md)   
 [用通配符搜索文本](search-text-with-wildcards.md)   
 [用正则表达式搜索文本](search-text-with-regular-expressions.md)  
  
  
