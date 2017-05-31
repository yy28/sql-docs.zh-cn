---
title: "跨数据库查询 | Microsoft Docs"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 41b00b196f6cfad66ae0e26bbb1516da2641d9b7
ms.openlocfilehash: 8289b02c3e15f1b299196c343503c9cb87387c6c
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="cross-database-queries"></a>跨数据库查询
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]开始，内存优化表不支持跨数据库事务。 不能从也访问某一内存优化表的相同事务或相同查询访问其他数据库。 可以轻松地将来自一个数据库的某个表中的数据复制到其他数据库的内存优化表中。  
  
 表变量不是事务性的。 因此，内存优化表变量可用于跨数据库查询中，并因此可以简化将数据从一个数据库中移到另一个数据库的内存优化表中的操作。 可以使用两个事务。 在第一个事务中，将数据从远程表插入到变量中。 在第二个事务中，将数据从变量插入到本地内存优化表中。  有关内存优化表变量的详细信息，请参阅 [通过使用内存优化更快获得临时表和表变量](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)。
  
## <a name="example"></a>示例
本示例说明了如何将数据从一个数据库传输到其他数据库中的内存优化表。

1. 创建测试对象。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中执行以下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  

    ```tsql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',    SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  尝试跨数据库查询。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中执行以下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
  
    ```tsql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    会收到以下错误信息：
    > 消息 41317，级别 16，状态 5  
    > 访问内存优化表或本机编译模块的用户事务无法访问多个用户数据库或数据库模型和 msdb，并且不能写入 master。

3.  创建内存优化表类型。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中执行以下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。

    ```tsql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  再次尝试跨数据库查询。  这一次源数据首先传输到内存优化表变量。  然后表变量数据传输到内存优化表。
    ```tsql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  

