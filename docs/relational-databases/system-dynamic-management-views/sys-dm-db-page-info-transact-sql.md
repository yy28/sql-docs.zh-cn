---
title: sys.dm_db_page_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: ''
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9f2e2d0b49f58eff2eac52103bddc6fda818aeb3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849275"
---
# <a name="sysdmdbpageinfo-transact-sql"></a>sys.dm_db_page_info (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在数据库中返回有关某一页的信息。  该函数将返回一行，其中包含标头信息的页面，其中包括`object_id`， `index_id`，和`partition_id`。  此函数无需使用`DBCC PAGE`在大多数情况下。

## <a name="syntax"></a>语法  
  
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>参数  
 *DatabaseId* |NULL |默认值  

 是数据库的 ID。 *DatabaseId*是**smallint**。 有效输入是数据库的 ID 号。 默认值为 NULL，但是发送此参数的 NULL 值将导致错误。
 
*FileId* |NULL |默认值

文件的 ID。 *FileId*是**int**。有效输入是由指定的数据库中的文件的 ID 号*DatabaseId*。 默认值为 NULL，但是发送此参数的 NULL 值将导致错误。

*PageId* |NULL |默认值

是的 ID。  *PageId*是**int**。有效输入是指定的文件中的页的 ID 号*FileId*。 默认值为 NULL，但是发送此参数的 NULL 值将导致错误。

*模式*|NULL |默认值

确定函数的输出详细的级别。 有限将返回 NULL 值的所有说明列中，详细将填入说明列。  默认值是限制。

## <a name="table-returned"></a>返回的表  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id |ssNoversion |数据库 ID |
|file_id |ssNoversion |文件 ID |
|page_id |ssNoversion |页面 ID |
|page_type |ssNoversion |页类型 |
|page_type_desc |Nvarchar(64) |页类型的说明 |
|page_flag_bits |Nvarchar(64) |页面页眉中的标志位 |
|page_flag_bits_desc |nvarchar(256) |页面页眉中的标志位说明 |
|page_type_flag_bits |Nvarchar(64) |页面页眉中的类型标志位 |
|page_type_flag_bits_desc |Nvarchar(64) |页面页眉中的类型标志位说明 |
|object_id |ssNoversion |拥有页上的对象的 ID |
|index_id |ssNoversion |索引 (0 表示堆数据页) 的 ID |
|partition_id |BIGINT |分区的 ID |
|alloc_unit_id |BIGINT |分配单元 ID |
|page_level |ssNoversion |在索引中页的级别 (叶 = 0) |
|slot_count |SMALLINT |槽的总数量 （使用和未使用） <br> 数据页中，此数字相当于的行数。 |
|ghost_rec_count |SMALLINT |标记为在页上的虚影记录数 <br> 虚影的记录是指已标记为删除但尚未删除。 |
|torn_bits |ssNoversion |每个检测残缺写操作的扇区的 1 位。 此外用于存储校验和 <br> 此值用于检测数据损坏 |
|is_iam_pg |bit |要指示页是 IAM 页位  |
|is_mixed_ext |bit |位指示中分配混合区 |
|pfs_file_id |SMALLINT |相应的 PFS 页的文件 ID |
|pfs_page_id |ssNoversion |相应的 PFS 页的页 ID |
|pfs_alloc_percent |ssNoversion |分配 %pfs 字节所示 |
|pfs_status |Nvarchar(64) |PFS 字节 |
|pfs_status_desc |Nvarchar(64) |PFS 字节的说明 |
|gam_file_id |SMALLINT |相应的 GAM 页的文件 ID |
|gam_page_id |ssNoversion |相应的 GAM 页的页 ID |
|gam_status |bit |位指示分配在 GAM 中 |
|gam_status_desc |Nvarchar(64) |GAM 状态位的说明 |
|sgam_file_id |SMALLINT |相应的 SGAM 页的文件 ID |
|sgam_page_id |ssNoversion |相应的 SGAM 页的页 ID |
|sgam_status |bit |位指示分配 SGAM 中 |
|sgam_status_desc |Nvarchar(64) |SGAM 状态位的说明 |
|diff_map_file_id |SMALLINT |相应的差异位图页的文件 ID |
|diff_map_page_id |ssNoversion |相应的差异位图页的页 ID |
|diff_status |bit |要指示是否更改差异状态位 |
|diff_status_desc |Nvarchar(64) |差异状态位的说明 |
|ml_file_id |SMALLINT |相应的最小日志记录位图页的文件 ID |
|ml_page_id |ssNoversion |相应的最小日志记录位图页的页 ID |
|ml_status |bit |若要指示页是否最小日志记录的位 |
|ml_status_desc |Nvarchar(64) |最小日志记录状态位的说明 |
|free_bytes |SMALLINT |在页上的可用字节数 |
|free_data_offset |ssNoversion |数据区域的末尾处的可用空间偏移量 |
|reserved_bytes |SMALLINT |保留的所有事务的可用字节数 (如果堆) <br> 虚影行 （如果索引的叶） 数 |
|reserved_xdes_id |SMALLINT |由 m_xdesID m_reservedCnt 到提供的空间 <br> 仅用于进行调试 |
|xdes_id |Nvarchar(64) |M_reserved 由提供的最新事务 <br> 仅用于进行调试 |
|prev_page_file_id |SMALLINT |前一页文件 ID |
|prev_page_page_id |ssNoversion |前一页的页 ID |
|next_page_file_id |SMALLINT |下一步的页文件 ID |
|next_page_page_id |ssNoversion |接下来页上的页 ID |
|管道 |SMALLINT |固定的大小的行的长度 |
|lsn |Nvarchar(64) |日志序列号 / 时间戳 |
|header_version |ssNoversion |页标头版本 |

## <a name="remarks"></a>备注
`sys.dm_db_page_info`动态管理函数返回类似的页面信息`page_id`， `file_id`， `index_id`，`object_id`等页标头中存在的。 此信息可用于故障排除和调试各种性能 （锁和闩锁争用） 和损坏问题。

`sys.dm_db_page_info` 可用来代替`DBCC PAGE`语句在许多情况下，但返回仅页标头的信息，不页的正文。 `DBCC PAGE` 仍将需要其中的页面的全部内容所需的用例。

## <a name="using-in-conjunction-with-other-dmvs"></a>在与其他 Dmv 一起使用
一个重要用例的`sys.dm_db_page_info`是将它加入与其他 dmv，用来显示页的信息。  为了帮助实现此用例，新列调用`page_resource`公开页 8 字节十六进制格式的信息已添加。 此列已添加到`sys.dm_exec_processes`和`sys.sysprocesses`，将添加到在将来根据需要其他 Dmv。

一个新的函数`sys.fn_PageResCracker`，采用`page_resource`作为输入，并输出包含一行`database_id`，`file_id`和`page_id`。  然后可以使用此函数以便之间的联接`sys.dm_exec_requests`或`sys.sysprocesses`和`sys.dm_db_page_info`。

## <a name="permissions"></a>Permissions  
需要`VIEW DATABASE STATE`数据库中的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. 显示页的所有属性
以下查询返回一个行的所有页面信息与给定`database_id`， `file_id`，`page_id`与默认模式 （受限） 结合使用

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdmdbpageinfo-with-other-dmvs"></a>B. 使用其他 Dmv sys.dm_db_page_info 

下面的查询返回每一行`wait_resource`公开的`sys.dm_exec_requests`包含非 null 的行 `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```

## <a name="see-also"></a>请参阅  
[动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   


