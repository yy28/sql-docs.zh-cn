---
title: 创建子查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e68809c7551e3c6711fadd9973c472dcb4e90307
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270623"
---
# <a name="create-subqueries-visual-database-tools"></a>创建子查询 (Visual Database Tools)
  可以将一个查询的结果用作另一个查询的输入。 可以将子查询的结果用作使用 IN(&#xA0;</ph>) 函数、EXISTS 运算符或 FROM 子句的语句。  
  
 若要创建子查询，可以在 SQL 窗格中将其直接输入，或者复制一个查询并将其粘贴到另一个查询中。  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>在 SQL 窗格中定义子查询  
  
1.  创建主查询。  
  
2.  在 SQL 窗格中选择 SQL 语句，然后使用“复制”将该查询移动到剪贴板中。  
  
3.  启动新查询，然后使用“粘贴”将第一个查询移动到新查询的 WHERE 或 FROM 子句中。  
  
     例如，假设有两个表（`products` 和 `suppliers`），您希望创建显示瑞典供应商的所有产品的查询。 在 `suppliers` 表中创建第一个查询以查找所有的瑞典供应商：  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
     使用“复制”命令将此查询移动到剪贴板中。 使用 `products` 表创建第二个查询，列出所需的产品信息：  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
     在 SQL 窗格中，向第二个查询中添加 WHERE 子句，然后从剪贴板粘贴第一个查询。 用括号将第一个查询括起来，最终结果类似于以下形式：  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>请参阅  
 [支持的查询类型&#40;可视化数据库工具&#41;](visual-database-tools.md)   
 [指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
