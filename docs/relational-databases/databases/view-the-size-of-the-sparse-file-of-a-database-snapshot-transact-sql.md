---
title: "查看数据库快照的稀疏文件大小 (Transact-SQL) | Microsoft Docs"
ms.date: 07/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 76e79c5662019c197c2cb11785ca250ac4ba2d0b
ms.lasthandoff: 04/11/2017

---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>查看数据库快照的稀疏文件大小 (Transact-SQL)
  本主题说明如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 来验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库文件是稀疏文件以及查看其实际大小和最大大小。 稀疏文件是 NTFS 文件系统的功能，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库快照使用。  
  
> [!NOTE]  
>  创建数据库快照期间，可以使用 CREATE DATABASE 语句中的文件名来创建稀疏文件。 这些文件名存储在 **sys.master_files** 中的 **physical_name** 列中。 在 **sys.database_files** 中（无论是在源数据库中还是在快照中）， **physical_name** 列中始终包含源数据库文件的名称。  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>验证数据库文件是稀疏文件  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上：  
  
     从数据库快照的 **sys.database_files** 中或从 **sys.master_files** 中选择 **is_sparse**列。 该值指示文件是否是稀疏文件，如下所示：  
  
     1 = 文件是稀疏文件。  
  
     0 = 文件不是稀疏文件。  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>查看稀疏文件的实际大小  
  
> [!NOTE]  
>  稀疏文件按 64 KB 的增量增长；因此，磁盘上稀疏文件的大小始终是 64 KB 的倍数。  
  
 若要查看磁盘上每个快照稀疏文件当前使用的字节数，请查询 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 动态管理视图的 **size_on_disk_bytes** 列。  
  
 若要查看稀疏文件占用的磁盘空间，在 Microsoft Windows 中右键单击文件，再单击“属性”****，然后查看“占用空间”****值。  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>查看稀疏文件的最大大小  
 稀疏文件最大只能增长到创建快照时相应的源数据库文件的大小。 若要了解此大小，可以使用下列方法之一：  
  
-   使用 Windows 命令提示符：  
  
    1.  使用 Windows **dir** 命令。  
  
    2.  在 Windows 中，选择稀疏文件，打开文件 **“属性”** 对话框，然后查看 **“大小”** 值。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上：  
  
     从数据库快照的 **sys.database_files** 中或从 **sys.master_files** 中选择 **size**列。 **“大小”** 列的值反映快照可以使用的最大空间（SQL 页数）；此值相当于 Windows 的 **“大小”** 字段，不同的是此值以文件中包含的 SQL 页数表示；大小（以字节为单位）为：  
  
     ( *number_of_pages* * 8192)  

## <a name="example"></a>示例
以下脚本将显示每个稀疏文件在磁盘上的大小 (KB)。  该脚本还将显示稀疏文件可增长到的最大大小 (MB)。  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中执行 Transact-SQL 脚本。

```tsql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>另请参阅  
 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats (Transact-SQL)](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

