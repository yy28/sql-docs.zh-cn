---
title: 创建表（教程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: eba540b70b444e06a861d2adb8a98e841ae62d35
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017301"
---
# <a name="creating-a-table-tutorial"></a>创建表（教程）
  若要创建表，您必须提供该表的名称以及该表中每个列的名称和数据类型。 指出每个列中是否允许空值，也是一种很好的做法。  
  
 大多数表有一个主键，主键由表的一列或多列组成。 主键始终是唯一的。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 将强制实施以下限制：表中的任何主键值都不能重复。  
  
 有关数据类型的列表以及每种数据类型的说明链接，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../includes/ssde-md.md)]可安装为区分大小写或不区分大小写。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 区分大小写进行安装，则对象名必须始终具有相同的大小写。 例如，名为 OrderData 的表与名为 ORDERDATA 的表是不同的表。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 按不区分大小写进行安装，则这两个表名被视为同一个表，而且该名称只能使用一次。  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>创建数据库以包含新表  
  
-   将下面的代码输入到查询编辑器窗口中。  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>将查询编辑器连接切换到 TestData 数据库  
  
-   在查询编辑器窗口中，键入以下代码，并执行它以更改与 `TestData` 数据库的连接。  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>创建表  
  
-   在查询编辑器窗口中，键入以下代码，并执行它以创建一个名为 `Products`的简单表。 该表中各列的名称为 `ProductID`、 `ProductName`、 `Price`和 `ProductDescription`。 `ProductID` 列是表的主键。 `int``varchar(25)`、 `money`和 `text` 都是数据类型。 当插入或更改行时，只有 `Price` 和 `ProductionDescription` 列可以不包含数据。 此语句包含称为架构的可选元素 (`dbo.`)。 架构是拥有表的数据库对象。 如果您是管理员，则 `dbo` 是默认架构。 `dbo` 代表数据库所有者。  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [插入和更新表中的数据（教程）](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>请参阅  
 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)  
  
  
