---
title: 创建表（教程）| Microsoft Docs
ms.custom: ''
ms.date: 04/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8a835c6da700059a15b782a9dd08cf6beabb37cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-2---creating-a-table"></a>第 1-2 课 - 创建表
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

若要创建表，您必须提供该表的名称以及该表中每个列的名称和数据类型。 指出每个列中是否允许空值，也是一种很好的做法。 若要创建表时，必须具有 `CREATE TABLE` 权限，以及对包含该表的架构的 `ALTER SCHEMA` 权限。 `db_ddladmin` 固定数据库角色具有这些权限。  
  
大多数表有一个主键，主键由表的一列或多列组成。 主键始终是唯一的。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 将强制实施以下限制：表中的任何主键值都不能重复。  
  
有关数据类型的列表以及每种数据类型的说明链接，请参阅[数据类型 (Transact-SQL)](../t-sql/data-types/data-types-transact-sql.md)。  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)]可安装为区分大小写或不区分大小写。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 区分大小写进行安装，则对象名必须始终具有相同的大小写。 例如，名为 OrderData 的表与名为 ORDERDATA 的表是不同的表。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 按不区分大小写进行安装，则这两个表名被视为同一个表，而且该名称只能使用一次。  
  
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
  
## <a name="see-also"></a>另请参阅  
[CREATE TABLE (Transact-SQL)](../t-sql/statements/create-table-transact-sql.md)  
  
  
  

