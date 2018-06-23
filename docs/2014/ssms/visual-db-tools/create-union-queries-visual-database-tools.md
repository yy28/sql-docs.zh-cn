---
title: 创建 UNION 查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fbfe0de4422aba4a73a5cabf16c42566c272a7d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123756"
---
# <a name="create-union-queries-visual-database-tools"></a>创建 UNION 查询 (Visual Database Tools)
  使用 UNION 关键字，可以在一个结果表中包含两个 SELECT 语句的结果。 任一 SELECT 语句返回的所有行都可合并到 UNION 表达式的结果中。 有关示例，请参阅[选择示例&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql)。  
  
> [!NOTE]  
>  “关系图”窗格只能显示一个 SELECT 子句。 因此，当使用 UNION 查询时，查询设计器将隐藏“表操作”窗格。  
  
### <a name="to-create-a-merged-select-query"></a>创建合并的 SELECT 查询  
  
1.  打开一个查询或创建一个新查询。  
  
2.  在 SQL 窗格中，键入有效的 UNION 表达式。  
  
     下面的示例是有效的 UNION 表达式。  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  在“查询设计器”菜单中，单击“执行 SQL”以运行该查询。  
  
     UNION 查询现在由查询设计器进行格式设置。  
  
## <a name="see-also"></a>请参阅  
 [支持的查询类型&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [设计查询和视图的操作指南主题&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [对查询执行基本操作&#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [联合&#40;Transact SQL&#41;](/sql/t-sql/language-elements/set-operators-union-transact-sql)  
  
  
