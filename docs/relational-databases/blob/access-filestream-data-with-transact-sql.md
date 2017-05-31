---
title: "使用 Transact-SQL 访问 FILESTREAM 数据 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 55caf01faba0be9c5277cbea435b256910e3dfc5
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="access-filestream-data-with-transact-sql"></a>使用 Transact-SQL 访问 FILESTREAM 数据
  本主题介绍如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT、UPDATE 和 DELETE 语句来管理 FILESTREAM 数据。  
  
> [!NOTE]  
>  本主题中的示例需要在 [创建启用 FILESTREAM 的数据库](../../relational-databases/blob/create-a-filestream-enabled-database.md) 和 [创建表以存储 FILESTREAM 数据](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)中创建的启用了 FILESTREAM 的数据库和表。  
  
##  <a name="ins"></a> 插入包含 FILESTREAM 数据的行  
 若要在支持 FILESTREAM 数据的表中插入一行，请使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 语句。 在 FILESTREAM 列中插入数据时，可以插入 NULL 或 **varbinary(max)** 值。  
  
### <a name="inserting-null"></a>插入 NULL  
 下面的示例说明了如何插入 `NULL`。 如果 FILESTREAM 值为 `NULL`，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不会在文件系统中创建文件。  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_1.sql)]  
  
### <a name="inserting-a-zero-length-record"></a>插入长度为零的记录  
 下面的示例说明了如何使用 `INSERT` 创建长度为零的记录。 如果您要获取文件句柄，但使用 Win32 API 来操作文件，这是非常有用的。  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_2.sql)]  
  
### <a name="creating-a-data-file"></a>创建数据文件  
 下面的示例说明了如何使用 `INSERT` 创建包含数据的文件。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将字符串 `Seismic Data` 转换为 `varbinary(max)` 值。 如果 Windows 文件尚未存在，FILESTREAM 将创建该文件。然后，在数据文件中添加数据。  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_3.sql)]  
  
 如果选择 `Archive`。`dbo.Records` 表中的所有数据，则结果与下表中显示的结果类似。 但是， `Id` 列将包含不同的 GUID。  
  
|ID|SerialNumber|恢复|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
  
##  <a name="upd"></a> 更新 FILESTREAM 数据  
 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更新文件系统文件中的数据；但是，如果必须以流的方式将大量数据传输到文件，您可能并不希望这样做。  
  
 下面的示例将文件记录中的所有文本替换为文本 `Xray 1`。  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_4.sql)]  
  
  
##  <a name="del"></a> 删除 FILESTREAM 数据  
 删除包含 FILESTREAM 字段的行时，会同时删除其基础文件系统文件。 删除行（从而删除文件）的唯一方式是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE 语句。  
  
 下面的示例说明了如何删除一行及其关联的文件系统文件。  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_5.sql)]  
  
 如果选择 `dbo.Archive` 表中的所有数据，则会发现该行已被删除。 您无法再使用关联的文件。  
  
> [!NOTE]  
>  基础文件是由 FILESTREAM 垃圾回收器删除的。  
  
  
## <a name="see-also"></a>另请参阅  
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [避免与 FILESTREAM 应用程序中的数据库操作冲突](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
