---
title: 包含或排除行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785a777571ef7659b1ae21a693e6754659a80e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63298593"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>包含或排除行 (Visual Database Tools)
  若要限制 SELECT 查询应返回的行数，请创建搜索条件或筛选条件。 在 SQL 中，搜索条件出现在语句的 WHERE 子句中，或者如果创建的是聚合查询，则搜索条件将出现在 HAVING 子句中。  
  
> [!NOTE]  
>  您也可使用搜索条件指示受“更新”、“插入结果”、“插入值”、“删除”或“生成表”查询影响的行。  
  
 当查询运行时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将检查搜索条件并将其应用到要搜索的表的每一行。 如果行满足搜索条件，就会包括在查询中。 例如，一个查找特定区域内所有雇员的搜索条件可以类似如下形式：  
  
```  
region = 'UK'  
```  
  
 若要建立在结果中包括行的准则，可以使用多个搜索条件。 例如，下面的搜索准则由两个搜索条件组成。 只有当行满足这两个条件时，查询才在结果集内包括该行。  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
 您可以用 AND 或 OR 组合这些条件。 上面的示例使用了 AND。 相反，下面的准则使用的是 OR。 结果集将包括满足其中任一个搜索条件或两个搜索条件都满足的所有行：  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
 您甚至可以组合对单个列的搜索条件。 例如，下面的准则组合了区域列的两个条件：  
  
```  
region = 'UK' OR region = 'US'  
```  
  
 有关组合搜索条件的详细信息，请参阅以下主题：  
  
-   [在“条件”窗格中组合搜索条件的约定 (Visual Database Tools)](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [为同一列指定多个搜索条件 (Visual Database Tools)](visual-database-tools.md)  
  
-   [为多个列指定多个搜索条件 (Visual Database Tools)](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [在 AND 优先时组合条件 (Visual Database Tools)](combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [在 OR 优先时组合条件 (Visual Database Tools)](combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>示例  
 下面是使用各种运算符和行条件的查询的一些示例：  
  
-   **文本** 单个文本值、数值、日期值或逻辑值。 下面的示例使用一个文本值在所有行中查找在英国的雇员：  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **列引用** 比较一个列中的值和另一个列中的值。 下面的示例在 `products` 表中搜索所有生产成本低于运输成本的行：  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **函数** 对函数的引用，数据库后端可以对其进行解析以计算搜索值。 此类函数可以是由数据库服务器定义的函数或者是返回标量值的用户定义函数。 下面的示例搜索今天所下的订单（GETDATE(&#xA0;</ph>) 函数返回当前日期）：  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** 下面的示例在 `authors` 表中搜索所有名字已存档的作者：  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **计算** 涉及文本、列引用或其他表达式的计算结果。 下面的示例在 `products` 表中搜索零售价格高于生产成本两倍的所有行：  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Visual Database Tools 的设计查询和视图操作指南主题&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [指定 Visual Database Tools &#40;搜索条件&#41;](specify-search-criteria-visual-database-tools.md)   
 [使用参数进行查询 (Visual Database Tools)](query-with-parameters-visual-database-tools.md)  
  
  
