---
title: "协调多个用户所做的更改 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 65aad0bfb2f6ce9e9ce5987ea47d4858d54c6e9e
ms.lasthandoff: 04/11/2017

---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>协调多个用户所做的更改 (Visual Database Tools)
在多用户环境中，多个用户可以同时对同一个对象进行更改。 当您在表或数据库关系图设计器中处理对象的结构时，可能会出现这种情况；对于查询和视图设计器的“结果”窗格内所返回结果中的值，也会出现这种情况。 这可能导致您需要解决的冲突。  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>表设计器或数据库关系图设计器中的冲突  
例如，当您在表设计器中处理某个表时，另一个用户可能会删除或重命名同一个表或相关的表。 尝试保存表时， [Database Changes Detected Dialog Box &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md) 会通知你，在打开该表之后数据库已经更新。  
  
该对话框还会显示一个列表，列出在您保存表时将受到影响的数据库对象。 此时，您可以执行以下操作之一：  
  
-   选择“是”****保存表并使用列表中的所有更改更新数据库。  
  
    此操作将影响共用相同数据库对象的表。 例如，假设编辑 `au`表中的`id` _ `titleauthors` 列，而另一个用户正在处理 `authors` 表，该表通过 `titleauthors` 列与 `au`\_`id` 表相关。 保存您的表将影响另一个用户的表。 与此类似，假设另一个用户为 `qty` 表中的 `sales` 列定义了一个 CHECK 约束。 如果您删除 `qty` 列并保存 `sales` 表，则另一个用户的 CHECK 约束将受到影响。  
  
-   选择“否”****取消保存操作。  
  
    您随后即可关闭该表而不进行保存。 当您重新打开该表时，它将与数据库中的相应内容匹配。  
  
-   选择“保存文本文件”****保存更改列表。  
  
    可以将“检测到数据库更改”****对话框中显示的一系列数据库更改保存为文本文件，以便调查其他用户的更改原因。 例如，如果另一个用户编辑了您标记为删除的表，则您可能希望研究在更新数据库之前是否应删除该表。  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>查询和视图设计器中的冲突  
如果运行查询或返回某视图的结果，则会在 [“结果”窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中显示数据。 多个用户可以同时对同一组数据进行操作，这便可能导致冲突。  
  
例如，假设您和同事分别运行查询以显示 `titleauthors` 表中的所有数据。 您的同事将返回的第一个记录中的名字由 Barb 改为 Barbara。 此时，数据库的相应字段将包含 Barbara，而您的结果集中仍会显示 Barb。 现在您键入 Barbara，然后在行外单击。 您将收到一条消息，询问要如何解决冲突。  
  
-   单击“是”****可以用你的更改来更新数据库。  
  
    这将重写您的同事的更改。  
  
-   单击“否”****可将结果集更新为数据库中的当前相应内容。  
  
    这将用您的同事的更改重写您的更改。  
  
-   单击“取消”****可继续编辑而不解决冲突。  
  
    在这种情况下，您将无法将更改提交到数据库。  
  
## <a name="see-also"></a>另请参阅  
[“检测到数据库更改”对话框 (Visual Database Tools)](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md)  
  

