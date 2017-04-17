---
title: "在聚合查询中使用列 (Visual Database Tools) | Microsoft Docs"
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
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 64aee66141249bc2a1848f6a65ec9683c73dc429
ms.lasthandoff: 04/11/2017

---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>在聚合查询中使用列 (Visual Database Tools)
创建聚合查询时，[查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)将进行某些假设以便可以构造有效的查询。 例如，如果创建聚合查询并将某个数据列标记为输出，则查询和视图设计器将自动将该列包含在 GROUP BY 子句中，以避免无意中试图在汇总中显示个别行的内容。  
  
## <a name="using-group-by"></a>使用“分组依据”  
查询和视图设计器在处理列时使用以下原则：  
  
-   在选择“分组依据”选项或向查询中添加聚合函数时，所有标记为输出或用于排序的列将自动添加到 GROUP BY 子句中。 如果列已经是聚合函数的一部分，则不会自动添加到 GROUP BY 子句中。  
  
    如果不想使某个特定列成为 GROUP BY 子句的一部分，必须在“条件”窗格的“分组依据”列中选择不同的选项以手动更改该设置。 然而，查询和视图设计器不会禁止您选择可能产生无法运行的查询的选项。  
  
-   如果在“条件”窗格或 SQL 窗格中手动向聚合函数添加查询输出列，则查询和视图设计器不能自动从查询中移除其他输出列。 因此，必须从查询输出中移除剩余的列，或使它们成为 GROUP BY 子句或聚合函数的一部分。  
  
向“条件”窗格的“筛选器”列中输入搜索条件时，查询和视图设计器将遵循以下规则：  
  
-   如果没有显示网格的“分组依据”列（因为尚未指定聚合查询），则搜索条件将放入 WHERE 子句中。  
  
-   如果已在聚合查询中，并在“分组依据”列中选择了 **Where** 选项，则搜索条件被放入 WHERE 子句中。  
  
-   如果“分组依据”列包含 **Where** 以外的任何值，则搜索条件将放入 HAVING 子句中。  
  
## <a name="using-the-having-and-where-clauses"></a>使用 HAVING 和 WHERE 子句  
以下原则描述如何在聚合查询的搜索条件中引用列。 通常，可以在搜索条件中使用列来筛选要汇总的行（WHERE 子句）或确定要在最终输出中显示的分组结果（HAVING 子句）。  
  
-   各个数据列可以出现在 WHERE 子句也可以出现在 HAVING 子句中，这取决于在查询中的其他地方使用这些数据列的方式。  
  
-   WHERE 子句用于选择行的子集以进行汇总和分组，因此在分组前应用 WHERE 子句。 所以，即使某个数据列不是 GROUP BY 子句的一部分或者不包含在聚合函数中，也可以在 WHERE 子句中使用该列。 例如，下面的语句选择所有超过 10.00 美元的书籍并求其平均价格：  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   如果创建的搜索条件所涉及的列同时也用于 GROUP BY 子句或聚合函数中，则该搜索条件既可以作为 WHERE 子句出现也可以作为 HAVING 子句出现，您可以在创建条件时决定以哪一种形式出现。 例如，下面的语句创建每个出版商的书籍的平均价格，然后显示平均价格超过 10.00 美元的出版商的平均值：  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   如果在搜索条件中使用聚合函数，则条件将涉及汇总，因此必须是 HAVING 子句的一部分。  
  
## <a name="see-also"></a>另请参阅  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  

