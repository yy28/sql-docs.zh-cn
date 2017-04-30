---
title: "增量搜索活动文档 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b3d3c79129936f6764261ec3f0ac1e0d54daf03d
ms.lasthandoff: 04/11/2017

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
>  有关键盘快捷键的完整列表，请参阅 [SQL Server Management Studio 键盘快捷键](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="see-also"></a>另请参阅  
 [搜索和替换](../../relational-databases/scripting/search-and-replace.md)   
 [交互式搜索文档](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用结果列表搜索文档](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [使用通配符搜索文本](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用正则表达式搜索文本](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
