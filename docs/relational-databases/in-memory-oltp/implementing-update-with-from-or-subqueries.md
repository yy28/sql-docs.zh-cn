---
title: 实现包含 FROM 或子查询的 UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 138f5b0e-f8a4-400f-b581-8062aebc62b6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: de3f3c760339b8459388c7f91af1dacf44d641ef
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="implementing-update-with-from-or-subqueries"></a>实现包含 FROM 或子查询的 UPDATE
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本机编译的 T-SQL 模块不支持 UPDATE 语句中的 FROM 子句和子查询（它们在 SELECT 中受支持）。 包含 FROM 子句的 UPDATE 语句通常用于基于表值参数 (TVP) 更新表格中的信息，或用于更新 AFTER 触发器的表格中的列。 

请参阅 [在本机编译的存储过程中实现 MERGE 功能](../../relational-databases/in-memory-oltp/implementing-merge-functionality-in-a-natively-compiled-stored-procedure.md)，了解基于 TVP 的更新方案。 

下面的示例阐释在触发器中执行的更新 - 表格的 LastUpdated 列更新为更新后的当前日期/时间。 该解决办法使用包含标识列的表变量和 WHILE 循环来循环访问表变量中的行，并执行单个更新。
  
下面是原始的 T-SQL UPDATE 语句：  
  
  
  
   ```
    UPDATE dbo.Table1  
        SET LastUpdated = SysDateTime()  
        FROM  
            dbo.Table1 t  
            JOIN Inserted i ON t.Id = i.Id;  
   ```
  
  

本部分中的示例 T-SQL 代码演示一个可提供良好性能的解决办法。 该解决办法在本机编译的触发器中实现。 对于该代码，需要注意的是：  
  
- 名为 dbo.Type1 的类型，这是一种内存优化表类型。  
- 触发器中的 WHILE 循环。  
  - 该循环从插入的行开始，一次检索一行。  
  
  
  
 ```
    DROP TABLE IF EXISTS dbo.Table1;  
    go  
    DROP TYPE IF EXISTS dbo.Type1;  
    go  
    -----------------------------  
    -- Table and table type
    -----------------------------
  
    CREATE TABLE dbo.Table1  
    (  
        Id           INT        NOT NULL  PRIMARY KEY NONCLUSTERED,  
        Column2      INT        NOT NULL,  
        LastUpdated  DATETIME2  NOT NULL  DEFAULT (SYSDATETIME())  
    )  
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
  
  
    CREATE TYPE dbo.Type1 AS TABLE  
    (  
        Id       INT NOT  NULL,  
        
        RowID    INT NOT  NULL  IDENTITY,  
        INDEX ix_RowID HASH (RowID) WITH (BUCKET_COUNT=1024)
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
    ----------------------------- 
    -- trigger that contains the workaround for UPDATE with FROM 
    -----------------------------  
  
    CREATE TRIGGER dbo.tr_a_u_Table1  
        ON dbo.Table1  
        WITH NATIVE_COMPILATION, SCHEMABINDING  
        AFTER UPDATE  
    AS 
    BEGIN ATOMIC WITH  
        (  
        TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
        LANGUAGE = N'us_english'  
        )  
        
      DECLARE @tabvar1 dbo.Type1;  
    
      INSERT @tabvar1 (Id)   
          SELECT Id FROM Inserted;  
    
      DECLARE  
          @i INT = 1,  @Id INT,  
          @max INT = SCOPE_IDENTITY();  
    
      ---- Loop as a workaround to simulate a cursor.
      ---- Iterate over the rows in the memory-optimized table  
      ----   variable and perform an update for each row.  
    
      WHILE @i <= @max  
      BEGIN  
          SELECT @Id = Id  
              FROM @tabvar1  
              WHERE RowID = @i;  
    
          UPDATE dbo.Table1  
              SET LastUpdated = SysDateTime()  
              WHERE Id = @Id;  
    
          SET @i += 1;  
      END  
    END  
    go  
    -----------------------------  
    -- Test to verify functionality
    -----------------------------  
  
    SET NOCOUNT ON;  
  
    INSERT dbo.Table1 (Id, Column2)  
        VALUES (1,9), (2,9), (3,600);  
    
    SELECT N'BEFORE-Update' AS [BEFORE-Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
  
    WAITFOR DELAY '00:00:01';  

    UPDATE dbo.Table1  
        SET   Column2 += 1  
        WHERE Column2 <= 99;  
  
    SELECT N'AFTER--Update' AS [AFTER--Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
    go  
    -----------------------------  
  
    /**** Actual output:  
  
    BEFORE-Update   Id   Column2   LastUpdated  
    BEFORE-Update   1       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   2       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   3     600      2016-04-20 21:18:42.8394659  
  
    AFTER--Update   Id   Column2   LastUpdated  
    AFTER--Update   1      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   2      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   3     600      2016-04-20 21:18:42.8394659  
    ****/  
  
  
 ```
