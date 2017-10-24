---
title: "插入和更新表 （教程） 中的数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 287e4e9b78b5c628dc94a21eea3ed26385c73649
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-3---inserting-and-updating-data-in-a-table"></a>课程 1-3-插入和更新表中的数据
现在已经创建了 **Products** 表，可以通过使用 INSERT 语句将数据插入到表中。 插入数据后，将通过使用 UPDATE 语句更改行的内容。 您将使用 UPDATE 语句的 WHERE 子句，以限制对单个行的更新。 这四条语句将输入以下数据。  
  
|ProductID|ProductName|价格|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
基本语法如下：INSERT、表名、列的列表、VALUES，然后是要插入的值的列表。 如果某行的前面有两个连字符，则指示该行为注释，编译器将忽略其文本。 在这种情况下，注释说明允许的语法变体。  
  
### <a name="to-insert-data-into-a-table"></a>将数据插入到表  
  
1.  执行以下语句，将一行插入到在上一个任务中创建的 `Products` 表中。 基本语法如下：  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  以下语句显示如何通过在字段列表（在圆括号中）中和值列表中均切换 `ProductID` 和 `ProductName` 的位置，更改提供参数的顺序。  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  以下语句演示，只要值是按正确顺序列出的，列的名称就是可选的。 此语法很常见，但是建议不要使用它，因为其他人了解您的代码可能会更困难。 `NULL` 为 `Price` 列指定，因为还不知道此产品的价格。  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  只要在默认架构中访问和更改表，架构名称就是可选的。 由于 `ProductDescription` 列允许 Null 值，而且没有提供值，因此可以从语句中完全删除 `ProductDescription` 列的名称和值。  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>更新 products 表  
  
1.  键入并执行以下 `UPDATE` 语句，将第二种产品的 `ProductName` 从 `Screwdriver`更改为 `Flat Head Screwdriver`。  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[读取表中的数据（教程）](../t-sql/lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>另请参阅  
[INSERT (Transact-SQL)](../t-sql/statements/insert-transact-sql.md)  
[UPDATE (Transact-SQL)](../t-sql/queries/update-transact-sql.md)  
  
  
  

