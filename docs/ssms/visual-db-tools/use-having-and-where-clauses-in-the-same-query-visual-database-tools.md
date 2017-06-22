---
title: "在同一查询中使用 HAVING 和 WHERE 子句 | Microsoft Docs"
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
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7a08a632df3d4f6b054f4b60cae2d4befc8c8745
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>在同一查询中使用 HAVING 和 WHERE 子句 (Visual Database Tools)
在某些情况下，在对整个组应用条件（使用 HAVING 子句）之前，可能希望排除组中的单个行（使用 WHERE 子句）。  
  
HAVING 子句与 WHERE 子句类似，但仅应用于整个组（即应用于表示组的结果集中的行），而 WHERE 子句应用于单个行。 查询可同时包含 WHERE 子句和 HAVING 子句。 在这种情况下：  
  
-   首先在“关系图”窗格中将 WHERE 子句应用于表或表值对象中的单个行。 只对满足 WHERE 子句中的条件的行进行分组。  
  
-   然后将 HAVING 子句应用于结果集中的行。 只有满足 HAVING 条件的组才会显示在查询输出中。 可以将 HAVING 子句仅应用于也同时出现在 GROUP BY 子句或聚合函数中的列。  
  
例如，假设您要联接 `titles` 和 `publishers` 表以创建一个查询，显示一组出版商的平均书籍价格。 您只希望看到一组特定出版商（也许只是加利福尼亚州的出版商）的平均价格。 甚至仅希望看到高于 10.00 美元的平均价格。  
  
在计算平均价格前，可通过包含 WHERE 子句建立第一个条件，该条件放弃不属于加利福尼亚的所有出版商。 第二个条件要求使用 HAVING 子句，因为该条件基于对数据进行分组和汇总的结果。 最终得到的 SQL 语句可能与以下代码类似：  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
可以在“条件”窗格中同时创建 HAVING 子句和 WHERE 子句。 默认情况下，如果为某个列指定搜索条件，则该条件将成为 HAVING 子句的一部分。 但是，您可以将该条件更改为 WHERE 子句。  
  
可以创建涉及同一列的 WHERE 子句和 HAVING 子句。 为此，必须向“条件”窗格添加该列两次，然后将一个实例指定为 HAVING 子句的一部分，并将另一个实例指定为 WHERE 子句的一部分。  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>在聚合查询中指定 WHERE 条件  
  
1.  为查询指定组。 有关详细信息，请参阅 [对查询结果中的行进行分组 (Visual Database Tools)](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)。  
  
2.  如果 WHERE 条件要基于的列不在“条件”窗格中，请添加该列。  
  
3.  除非数据列是 GROUP BY 子句的一部分或包含在聚合函数中，否则请清除“输出”列。  
  
4.  在“筛选器”列中，指定 WHERE 条件。 查询和视图设计器会将该条件添加到 SQL 语句的 HAVING 子句中。  
  
    > [!NOTE]  
    > 此过程的示例中显示的查询将联接 `titles` 和 `publishers`这两张表。  
  
    此时在查询中，SQL 语句包含一个 HAVING 子句：  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  在“分组依据”列中，从组和汇总选项的列表中选择 **Where**。 查询和视图设计器将从 SQL 语句的 HAVING 子句中移除该条件，并将其添加到 WHERE 子句中。  
  
    SQL 语句更改为包含 WHERE 子句：  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>另请参阅  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  

