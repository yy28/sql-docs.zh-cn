---
title: sys.fn_virtualfilestats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 45bfe4b78d751ab413bd87fe9629fc3521826612
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnvirtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回数据库文件（包括日志文件）的 I/O 统计信息。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此信息也会提供[sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md)动态管理视图。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>参数  
 *database_id* |NULL  
 是数据库的 ID。 database_id 的数据类型为 int，无默认值。 指定 NULL 可返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中所有数据库的信息。  
  
 *file_id* |NULL  
 文件的 ID。 *file_id*是**int**，无默认值。 指定 NULL 可为数据库中的所有文件返回信息。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DbId**|**int**|数据库 ID。|  
|**FileId**|**int**|文件 ID。|  
|**TimeStamp**|**bigint**|提取数据时的数据库时间戳。 **int**在之前的版本[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]。 |  
|**NumberReads**|**bigint**|对文件发出的读取次数。|  
|**BytesRead**|**bigint**|对文件发出的读取字节数。|  
|**IoStallReadMS**|**bigint**|用户等待文件的读取 I/O 完成所费的总时间（以毫秒为单位）。|  
|**NumberWrites**|**bigint**|对文件的写入次数。|  
|**BytesWritten**|**bigint**|对文件写入的字节数。|  
|**IoStallWriteMS**|**bigint**|用户等待文件的写入 I/O 完成所费的总时间（以毫秒为单位）。|  
|**IoStallMS**|**bigint**|总和**IoStallReadMS**和**IoStallWriteMS**。|  
|**文件句柄**|**bigint**|文件句柄的值。|  
|**BytesOnDisk**|**bigint**|磁盘上的物理文件大小（以字节为单位）。<br /><br /> 对于数据库文件，这将是相同的值**大小**中**sys.database_files**，但是在字节，而不是页表示。<br /><br /> 对于数据库快照备用文件，它是操作系统用于文件的空间。|  
  
## <a name="remarks"></a>注释  
 **fn_virtualfilestats**是提供统计信息，如 I/o 总数的表值函数执行的文件系统。 可使用该函数来帮助跟踪用户读取文件或写入到文件必须等待的时间长度。 该函数还可帮助您识别出发生了大量 I/O 活动的文件。  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. 显示数据库的统计信息  
 以下示例显示 ID 为 `1` 的数据库中的文件 ID 1 的统计信息。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. 显示命名数据库和文件的统计信息  
 以下示例显示 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库中日志文件的统计信息。 系统函数`DB_ID`用于指定*database_id*参数。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. 显示所有数据库和文件的统计信息  
 以下示例显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例内所有数据库中的所有文件的统计信息。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DB_ID &#40;Transact SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX (Transact-SQL)](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
