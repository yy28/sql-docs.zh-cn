---
title: 对查询结果中的行进行分组 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c66729fee4be279fe48ce657d85e4b2dbb97fef1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>对查询结果中的行进行分组 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果希望创建小计或显示表的子集的其他摘要信息，可使用聚合查询创建组。 各组可对表中具有相同值的所有行的数据进行汇总。  
  
例如，假设希望看到 `titles` 表中某书籍的平均价格，并将结果按出版商分组。 为此，需要按出版商（例如 `pub_id`）对查询进行分组。 声称的查询输出结果可能类似以下形式：  
  
![查询结果：按出版商分组的平均价格](../../ssms/visual-db-tools/media/dv3w9e1.gif "查询结果：按出版商分组的平均价格")  
  
当对数据进行分组时，只能显示汇总数据和分组数据，例如：  
  
-   分组列（GROUP BY 子句中显示的列）的值。 在上面的示例中， `pub_id` 就是分组列。  
  
-   由类似于 SUM(&#xA0;</ph>) 和 AVG(&#xA0;</ph>) 的聚合函数生成的值。 在上面的示例中，第二列就是对 `price` 列应用 AVG( ) 函数而生成的。  
  
您无法显示单个行的值。 例如，如果仅按出版商分组，则无法同时在查询中显示单个书名。 因此，如果向查询输出中添加列，则 [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 会自动将其添加到 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)内语句的 GROUP BY 子句中。 如果希望对某列进行聚合，则可为该列指定聚合函数。  
  
如果按多个列进行分组，查询中的每一组都会显示所有分组列的聚合值。  
  
例如，下面对 `titles` 表进行的查询按出版商 (`pub_id`) 和书籍类型 (`type`) 进行分组。 查询结果将按出版商进行排序，并会显示相应出版商出版的各种不同类型书籍的摘要信息：  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
生成的输出结果可能类似以下形式：  
  
![查询结果：按出版商和类型分组的价格](../../ssms/visual-db-tools/media/dv3w9e2.gif "查询结果：按出版商和类型分组的价格")  
  
### <a name="to-group-rows"></a>对行进行分组  
  
1.  通过将要汇总的表添加到“关系图”窗格中来启动查询。  
  
2.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“添加分组依据”。 查询和视图设计器会在“条件”窗格的网格中添加一个“分组依据”列。  
  
3.  将要分组的一列或多列添加到“条件”窗格中。 如果希望列显示在查询输出中，请确保为输出选中了“输出”列。  
  
    查询和视图设计器将在 SQL 窗格内的语句中添加 GROUP BY 子句。 例如，SQL 语句可能类似以下形式：  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  将要聚合的一列或多列添加到“条件”窗格中。 确保将该列标记为输出。  
  
5.  在要进行聚合的列的“分组依据”网格单元格中，选择适当的聚合函数。  
  
    查询及视图设计器将自动为要汇总的列分配列别名。 您可以用更有意义的名称替换这一自动生成的别名。 有关详细信息，请参阅 [创建列别名 (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)。  
  
    ![将列别名添加到查询结果集](../../ssms/visual-db-tools/media/dv3w9e3.gif "将列别名添加到查询结果集")  
  
    **SQL** 窗格中的相应语句可能类似以下形式：  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>另请参阅  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
