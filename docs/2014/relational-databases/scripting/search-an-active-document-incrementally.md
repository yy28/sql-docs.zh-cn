---
title: 增量搜索活动文档 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1024f140102369bdf45168a67c64cc1fb467d39c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129426"
---
# <a name="search-an-active-document-incrementally"></a>增量搜索活动文档
  您可以通过输入文字来对单个文档或窗口执行渐进式搜索。 搜索操作会突出显示与在文档或窗口的渐进式搜索过程中输入的字符相匹配的第一个字符集。 渐进式搜索会自动搜索文档或窗口内的所有文字，但隐藏文字除外。  
  
 对于 **“大小写匹配”** 选项，渐进式搜索将使用上一次搜索的条件。 例如，如果使用“在文件中查找”对话框跨多个文件执行搜索，并选择“大小写匹配”，然后执行渐进式搜索，则此搜索将区分大小写。  
  
### <a name="to-search-incrementally"></a>执行渐进式搜索  
  
1.  打开您要搜索的文件或窗口。  
  
2.  在 **“编辑”** 菜单中，指向 **“高级”**，然后单击 **“渐进式搜索”**。  
  
     光标图标会变为带箭头的望远镜，指示搜索方向，并且状态栏显示“渐进式搜索”。  
  
3.  开始键入文本字符串。  
  
     当编辑器突出显示此文本的第一个匹配项时，状态栏会显示您正在输入的文本。 编辑器会随着您的继续键入而移动到下一个匹配项并使其突出显示。 如果没有匹配项，状态栏会显示以下信息。  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 渐进式搜索从文档中的当前位置向下自左至右执行。 可以使用键盘快捷键完成渐进式搜索。  
  
> [!NOTE]  
>  有关键盘快捷键的完整列表，请参阅 [SQL Server Management Studio 键盘快捷键](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="see-also"></a>请参阅  
 [搜索和替换](search-and-replace.md)   
 [交互式搜索文档](search-documents-interactively.md)   
 [使用结果列表搜索文档](search-documents-using-results-lists.md)   
 [使用通配符搜索文本](search-text-with-wildcards.md)   
 [使用正则表达式搜索文本](search-text-with-regular-expressions.md)  
  
  