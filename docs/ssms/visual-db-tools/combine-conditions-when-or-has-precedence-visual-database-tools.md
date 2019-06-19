---
title: 在 OR 优先时组合条件 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5757d32093ab6547092d967f1d9fcf8c94323cf0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65093359"
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>在 OR 优先时组合条件 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要用 OR 链接条件，并使其优先级高于用 AND 链接的条件，则必须为每个 OR 条件重复 AND 条件。  
  
例如，假设要查找在公司工作五年以上的低级职位或已退休的所有雇员。 此查询需要三个条件，其中一个条件使用 AND 链接到另外两个条件：  
  
-   雇佣日期是在五年前的雇员，AND  
  
-   职位等级为 100 或其状态为“R”（表示已退休）的雇员。  
  
以下过程说明如何在“条件”窗格中创建此类查询。  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>在 OR 优先时组合条件  
  
1.  在 [“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，添加要搜索的数据列。 如果希望使用通过 AND 链接的两个或多个条件搜索同一列，则对于每个要搜索的值都必须将该数据列名添加到网格中一次。  
  
2.  创建将由 OR 链接的条件，方法是将第一个条件输入到“筛选器”  网格列中，然后将第二个（以及后续条件）输入单独的“或...”  列中。 例如，若要用 OR 链接搜索 `job_lvl` 和 `status` 列的条件，请在“筛选器”  列中为 `job_lvl` 输入 `= 100`，在“或...”  列中为 `status` 输入 `= 'R'`。  
  
    在网格中输入这些值后，就会在 SQL 窗格内的语句中生成以下 WHERE 子句：  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  通过为每个 OR 条件输入一次 AND 条件来创建 AND 条件。 将每个项放在其所对应的 OR 条件所在的同一网格列中。 例如，若要添加搜索 `hire_date` 列并应用于两个 OR 条件的 AND 条件，请在“条件”列和“或...”  列中均输入 `< '1/1/91'`。  
  
    在网格中输入这些值后，就会在 SQL 窗格内的语句中生成以下 WHERE 子句：  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > 可通过添加一次 AND 条件，再使用“编辑”  菜单中的“剪切”  和“粘贴”  命令对其他 OR 条件重复此操作来重复 AND 条件。  
  
查询和视图设计器创建的 WHERE 子句等效于以下 WHERE 子句，后者使用括号指定 OR 优先于 AND：  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> 如果以上面显示的格式在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中输入搜索条件，然后在“关系图”或“条件”窗格中对该查询进行更改，则查询和视图设计器将重新创建 SQL 语句，以使其形式与显式分配到两个 OR 条件的 AND 条件相匹配。  
  
## <a name="see-also"></a>另请参阅  
[在“条件”窗格中组合搜索条件的约定 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
