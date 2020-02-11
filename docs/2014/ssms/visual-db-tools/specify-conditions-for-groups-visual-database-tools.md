---
title: 为组指定条件 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc0f9319e4d598548111b44b1a10542773a7daa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63049137"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>为组指定条件 (Visual Database Tools)
  可以通过指定应用于整个组的条件（HAVING 子句）来限制查询中出现的组。 对数据进行分组和聚合后，将应用 HAVING 子句中的条件。 只有满足条件的组才会出现在查询中。  
  
 例如，您可能希望看到 `titles` 表中每个出版商出版的所有书籍的平均价格，但只显示平均价格超过 10.00 美元的部分。 在这种情况下，您可以为 HAVING 子句指定如下条件： `AVG(price) > 10`。  
  
> [!NOTE]  
>  在某些情况下，在对整个组应用条件之前，可能希望排除组中的单个行。 有关详细信息，请参阅[在同一查询中使用 HAVING 和 WHERE 子句 (Visual Database Tools)](visual-database-tools.md)。  
  
 通过使用 AND 和 OR 链接条件，可以为 HAVING 子句创建复杂的条件。 有关在搜索条件中使用 AND 和 OR 的详细信息，请参阅[为一列指定多个搜索条件 (Visual Database Tools)](specify-multiple-search-conditions-for-one-column-visual-database-tools.md)。  
  
### <a name="to-specify-a-condition-for-a-group"></a>为组指定条件  
  
1.  为查询指定组。 有关详细信息，请参阅[对查询结果中的行进行分组 (Visual Database Tools)](group-rows-in-query-results-visual-database-tools.md)。  
  
2.  如果条件要基于的列不在“[条件](criteria-pane-visual-database-tools.md)”窗格中，请添加该列。 （大多数情况下，该条件所涉及的列已经是组或汇总列。）不能使用未包含在聚合函数或 GROUP BY 子句中的列。  
  
3.  在“筛选器”  列中，指定要对组应用的条件。  
  
     [查询和视图设计器](query-and-view-designer-tools-visual-database-tools.md)将自动在“[SQL 窗格](sql-pane-visual-database-tools.md)”的语句中创建 HAVING 子句，如下例所示：  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
  
    ```  
  
4.  对于要指定的每个其他条件重复第 2 和第 3 步。  
  
## <a name="see-also"></a>另请参阅  
 [对查询结果进行排序和分组 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
  
