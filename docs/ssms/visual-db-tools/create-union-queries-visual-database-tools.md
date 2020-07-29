---
title: 创建 UNION 查询
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 9a7a274c092a98cbe63313f633ec37fc4377aa75
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000018"
---
# <a name="create-union-queries-visual-database-tools"></a>创建 UNION 查询 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
使用 UNION 关键字，可以在一个结果表中包含两个 SELECT 语句的结果。 任一 SELECT 语句返回的所有行都可合并到 UNION 表达式的结果中。 例如，请参阅 [SELECT 示例 (Transact-SQL)](https://msdn.microsoft.com/9b9caa3d-e7d0-42e1-b60b-a5572142186c)。  
  
> [!NOTE]  
> “关系图”窗格只能显示一个 SELECT 子句。 因此，当使用 UNION 查询时，查询设计器将隐藏“表操作”窗格。  
  
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
  
3.  在“查询设计器”  菜单中，单击“执行 SQL”  以运行该查询。  
  
    UNION 查询现在由查询设计器进行格式设置。  
  
## <a name="see-also"></a>另请参阅  
[支持的查询类型](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和查看操作说明主题](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](https://msdn.microsoft.com/607c296f-8a6a-49bc-975a-b8d0c0914df7)