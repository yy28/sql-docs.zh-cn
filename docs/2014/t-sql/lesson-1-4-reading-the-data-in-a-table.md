---
title: 读取表中的数据（教程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0649e167ebaa90267422594ccd193ba468838e6f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182007"
---
# <a name="reading-the-data-in-a-table-tutorial"></a>读取表中的数据（教程）
  使用 SELECT 语句可以读取表中的数据。 SELECT 语句是最重要的 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句之一，其语法有许多变体。 在本教程中，您将使用五个简单版本。  
  
### <a name="to-read-the-data-in-a-table"></a>读取表中的数据  
  
1.  键入并执行以下语句以读取 `Products` 表中的数据。  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  您可以使用星号选择表中的所有列。 这通常用于即席查询中。 您应该在永久代码中提供列的列表，以便语句将返回预测列，即使稍后将新列添加到表中也是如此。  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  可以省略不希望返回的列。 列将按列出它们的顺序返回。  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  使用 `WHERE` 子句可以限制返回给用户的行。  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  您可以在返回列中的值时使用它们。 以下示例对 `Price` 列执行数学运算。 除非通过使用 `AS` 关键字提供一个名称，否则以此方式更改的列将没有名称。  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>SELECT 语句中的有用函数  
 有关可以在 SELECT 语句中用来处理数据的一些函数的信息，请参阅下列主题：  
  
|||  
|-|-|  
|[字符串函数 (Transact-SQL)](/sql/t-sql/functions/string-functions-transact-sql)|[日期和时间数据类型及函数 (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|  
|[数学函数 (Transact-SQL)](/sql/t-sql/functions/mathematical-functions-transact-sql)|[文本和图像函数&#40;Transact SQL&#41;](/sql/t-sql/functions/text-and-image-functions-textptr-transact-sql)|  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [摘要：创建数据库对象](lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>请参阅  
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)  
  
  
