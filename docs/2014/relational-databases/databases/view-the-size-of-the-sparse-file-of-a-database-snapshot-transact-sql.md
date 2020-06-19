---
title: 查看数据库快照的稀疏文件大小 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
ms.openlocfilehash: 424399b9915c8e7e26e1076fd2e553aafe06fcf0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969927"
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
  
 要查看磁盘上每个快照稀疏文件当前使用的字节数，请查询 sys.dm_io_virtual_file_stats 动态管理视图的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][size_on_disk_bytes](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) 列****。  
  
 若要查看稀疏文件占用的磁盘空间，在 Microsoft Windows 中右键单击文件，再单击“属性”  ，然后查看“占用空间”  值。  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>查看稀疏文件的最大大小  
 稀疏文件最大只能增长到创建快照时相应的源数据库文件的大小。 若要了解此大小，可以使用下列方法之一：  
  
-   使用 Windows 命令提示符：  
  
    1.  使用 Windows **dir** 命令。  
  
    2.  在 Windows 中，选择稀疏文件，打开文件 **“属性”** 对话框，然后查看 **“大小”** 值。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上：  
  
     从数据库快照的 **sys.database_files** 中或从 **sys.master_files** 中选择 **size**列。 **“大小”** 列的值反映快照可以使用的最大空间（SQL 页数）；此值相当于 Windows 的 **“大小”** 字段，不同的是此值以文件中包含的 SQL 页数表示；大小（以字节为单位）为：  
  
     ( *number_of_pages* * 8192)  
  
## <a name="see-also"></a>另请参阅  
 [数据库快照 &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [sys. fn_virtualfilestats &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [sys. database_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
