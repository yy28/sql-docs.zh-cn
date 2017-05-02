---
title: "在 AND 优先时组合条件 (Visual Database Tools) | Microsoft Docs"
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
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c8d08365ac129d8b43e49d166ffccd866396c37
ms.lasthandoff: 04/11/2017

---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>在 AND 优先时组合条件 (Visual Database Tools)
若要使用 AND 组合条件，应向查询中添加两次列，一个条件一次。 若要使用 OR 组合条件，可将第一个条件放在“筛选器”列中，并将其他条件放在“或...”****列中。  
  
例如，假设要查找在公司的低级职位工作五年以上的雇员，或查找中级职位的雇员而不考虑其雇佣日期。 此查询需要三个条件，其中两个条件用 AND 链接：  
  
-   雇佣日期在五年之前并且职位等级为 100 的雇员。  
  
    - 或 -  
  
-   职位等级为 200 的雇员。  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>在 AND 优先时组合条件  
  
1.  在 [“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，添加要搜索的数据列。 如果希望使用通过 AND 链接的两个或多个条件搜索同一列，则对于每个要搜索的值都必须将该数据列名添加到网格中一次。  
  
2.  在“筛选器”****列中，输入要用 AND 链接的所有条件。 例如，若要用 AND 链接搜索 `hire_date` 列和 `job_lvl` 列的条件，请在“筛选器”列中分别输入值 `< '1/1/91'` 和 `= 100`。  
  
    这些网格项在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)内的语句中生成以下 WHERE 子句：  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  在“或...”****网格列中，输入要用 OR 链接的条件。 例如，若要添加在 `job_lvl` 列中搜索其他值的条件，请在“或...”****列中输入其他值，例如 `= 200`。  
  
    在“或...”****列中添加值时，将向 SQL 窗格内的语句中的 WHERE 子句中添加另一个条件：  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>另请参阅  
[在 OR 优先时组合条件 (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[在“条件”窗格中组合搜索条件的约定 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[输入搜索值的规则 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

