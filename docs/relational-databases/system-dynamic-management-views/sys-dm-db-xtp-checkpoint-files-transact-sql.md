---
title: sys.dm_db_xtp_checkpoint_files (TRANSACT-SQL) |Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 641519b479f89609e72e52bb1b1526dc09a976a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637435"
---
# <a name="sysdmdbxtpcheckpointfiles-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  显示有关检查点文件的信息，包括文件大小、物理位置和事务 ID。  
  
> **注意：** 未关闭，s 的状态列的当前检查点`ys.dm_db_xtp_checkpoint_files`的新文件将为 UNDER CONSTRUCTION。 检查点会自动关闭时没有足够的事务日志增长，因为最后一个检查点，或者如果发出`CHECKPOINT`命令 ([检查点&#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md))。  
  
 内存优化文件组在内部使用仅限追加的文件来存储内存中表的插入和删除行。 有两种类型的文件。 数据文件包含插入的行，而差异文件包含对已删除的行的引用。 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 大大不同于较新版本和更低时在主题中讨论[SQL Server 2014](#bkmk_2014)。  
  
 有关详细信息，请参阅[创建和管理存储的内存优化对象](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)。  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本  
 下表描述的列`sys.dm_db_xtp_checkpoint_files`开头**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|数据或差异文件所属的容器 ID（在 sys.database_files 中表示为类型为 FILESTREAM 的文件）。 中与 file_id 联接[sys.database_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。|  
|container_guid|**uniqueidentifier**|容器，该根、 数据或差异文件的 GUID。 与 file_guid sys.database_files 表中联接。|  
|checkpoint_file_id|**uniqueidentifier**|检查点文件的 GUID。|  
|relative_file_path|**nvarchar(256)**|相对于容器映射到文件的路径。|  
|file_type|**smallint**|对于免费为-1<br /><br /> 0 表示数据文件。<br /><br /> 1 表示差异文件。<br /><br /> 2 根文件<br /><br /> 3 个大型数据文件|  
|file_type_desc|**nvarchar(60)**|保持为可用的免费全部文件是可用于分配。 由系统根据预期需求的大小不同可用的文件。 最大大小为 1 GB。<br /><br /> 数据-数据文件包含已插入到内存优化表的行。<br /><br /> 增量的增量文件包含对已删除的数据文件中的行的引用。<br /><br /> 根的根文件包含内存优化表和本机编译的对象的系统元数据。<br /><br /> 大型数据的大型数据文件包含值插入到中 （n)varchar(max) 和 varbinary （max） 列，以及内存优化表的列存储索引中的列段。|  
|internal_storage_slot|**int**|内部存储数组中的文件的索引。 根或 1 以外的其他状态，则为 NULL。|  
|checkpoint_pair_file_id|**uniqueidentifier**|相应的数据或差异文件。 对于根为 NULL。|  
|file_size_in_bytes|**bigint**|在磁盘上文件的大小。|  
|file_size_used_in_bytes|**bigint**|对于仍在填充的检查点文件对，此列将在下一个检查点的后面更新。|  
|logical_row_count|**bigint**|对于数据，插入的行数。<br /><br /> 为增量后 drop table, 删除行数。<br /><br /> 对于根，则为 NULL。|  
|state|**smallint**|0 – PRECREATED<br /><br /> 1-正在构造<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 8-等待日志截断|  
|state_desc|**nvarchar(60)**|PRECREATED – 一个检查点文件数是预先分配，以便尽量减少或消除任何等待时间，从而在执行事务时分配新文件。 这些预创建的文件的大小，具体取决于工作负荷，估计需要有所不同，但它们不包含任何数据。 这是使用 MEMORY_OPTIMIZED_DATA 文件组的数据库中存储开销。<br /><br /> 正在构造的这些检查点文件正处于构造中，这意味着它们将被填充基于由数据库生成的日志记录，并且尚不是检查点的一部分。<br /><br /> ACTIVE-这些包含来自以前关闭的检查点插入/已删除行。 它们包含的区域应用在数据库重新启动的事务日志的活动部分之前读取到内存中表的内容。 我们预计这种大小的大约 2 倍的内存中大小的内存优化表，假定合并操作与事务工作负荷保持这些检查点文件。<br /><br /> MERGE TARGET – 合并操作-这些检查点文件的目标存储从合并策略标识的源文件的合并的数据行。 合并已安装之后，MERGE TARGET 转换为 ACTIVE 状态。<br /><br /> 等待日志截断 – 后合并已安装并且 MERGE TARGET CFP 属于持久检查点，合并源检查点文件转换为此状态。 对内存优化表的数据库正确操作，需要处于此状态的文件。  例如，用于从持久检查点恢复以便及时返回。|  
|lower_bound_tsn|**bigint**|在文件中的事务的下限如果状态不在 （1，3），则为 null。|  
|upper_bound_tsn|**bigint**|在文件中的事务的上限如果状态不在 （1，3），则为 null。|  
|begin_checkpoint_id|**bigint**|开始检查点的 ID。|  
|end_checkpoint_id|**bigint**|最终检查点的 ID。|  
|last_updated_checkpoint_id|**bigint**|更新此文件的最后一个检查点的 ID。|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = &GT; UNENCRTPTED<br /><br /> 1 = &GT; 密钥 1 加密<br /><br /> 2 = &GT; 加密使用密钥 2。 仅对活动文件有效。|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 下表描述的列`sys.dm_db_xtp_checkpoint_files`，对于**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|数据或差异文件所属的容器 ID（在 sys.database_files 中表示为类型为 FILESTREAM 的文件）。 中与 file_id 联接[sys.database_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。|  
|container_guid|**uniqueidentifier**|数据或差异文件所属的容器的 GUID。|  
|checkpoint_file_id|**GUID**|数据或差异文件的 ID。|  
|relative_file_path|**nvarchar(256)**|数据或差异文件的路径（相对于容器的位置）。|  
|file_type|**tinyint**|0 表示数据文件。<br /><br /> 1 表示差异文件。<br /><br /> 如果状态列设置为 7，则为 NULL。|  
|file_type_desc|**nvarchar(60)**|文件类型： DATA_FILE、 DELTA_FILE 或 NULL 如果状态列设置为 7。|  
|internal_storage_slot|**int**|内部存储数组中的文件的索引。 如果状态列不是 2 或 3，则为 NULL。|  
|checkpoint_pair_file_id|**uniqueidentifier**|对应的数据或差异文件。|  
|file_size_in_bytes|**bigint**|所用文件的大小。 如果状态列设置为 5、6 或 7，则为 NULL。|  
|file_size_used_in_bytes|**bigint**|所用文件的已用大小。 如果状态列设置为 5、6 或 7，则为 NULL。<br /><br /> 对于仍在填充的检查点文件对，此列将在下一个检查点的后面更新。|  
|inserted_row_count|**bigint**|数据文件中的行数。|  
|deleted_row_count|**bigint**|差异文件中删除的行数。|  
|drop_table_deleted_row_count|**bigint**|删除表影响的数据文件中的行数。 当状态列等于 1 时，应用于数据文件。<br /><br /> 显示从已删除表中删除的行计数。 在对已删除表中的行完成内存垃圾回收并且实施了检查点之后，汇总 drop_table_deleted_row_count 统计信息。 如果您在此列中反映删除表统计信息之前重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则统计信息会在恢复过程中更新。 恢复过程不会从已删除表中加载行。 已删除表的统计信息会在加载阶段中进行汇总并在此列中进行报告（恢复完成时）。|  
|state|**int**|0 – PRECREATED<br /><br /> 1 - UNDER CONSTRUCTION<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 4 – MERGED SOURCE<br /><br /> 5 – REQUIRED FOR BACKUP/HA<br /><br /> 6 – IN TRANSITION TO TOMBSTONE<br /><br /> 7 – TOMBSTONE|  
|state_desc|**nvarchar(60)**|PRECREATED – 一小组数据和差异文件对（也称为检查点文件对 (CFP)）保持预分配状态，以便尽量减少或消除任何等待时间，从而在执行事务时分配新文件。 针对数据文件的预分配 CFP 的完整大小是 128MB，而针对差异文件的预分配 CFP 的完整大小是 8 MB，但不包含任何数据。 CFP 的数目计算为逻辑处理器或计划程序的数目（每个核心一个，无最大值），最小值为 8。 这是具有内存优化表的数据库中的固定存储开销。<br /><br /> UNDER CONSTRUCTION – 存储自上个检查点以来新插入和可能删除的数据行的 CFP 集。<br /><br /> ACTIVE - 这些包含来自以前关闭的检查点的已插入和已删除行。 这些 CFP 包含数据库重新启动时在应用事务日志的活动部分前所需的所有已插入和已删除行。 这些 CFP 的大小大约是内存优化表在内存中的大小的 2 倍（假定合并操作是针对事务工作负荷的当前操作）。<br /><br /> MERGE TARGET – CFP 存储由合并策略标识的 CFP 中的合并数据行。 合并已安装之后，MERGE TARGET 转换为 ACTIVE 状态。<br /><br /> MERGED SOURCE – 合并操作已安装之后，源 CFP 标记为 MERGED SOURCE。 请注意，合并策略计算器可能标识多个合并，但是一个 CFP 只能参与一个合并操作。<br /><br /> REQUIRED FOR BACKUP/HA – 合并已安装并且 MERGE TARGET CFP 属于持久检查点之后，合并源 CFP 转换为此状态。 为保证具有内存优化表的数据库的运行正确性，需要处于此状态的 CFP。  例如，用于从持久检查点恢复以便及时返回。 在日志截断点移出其事务范围后，可以将 CFP 标为进行垃圾回收。<br /><br /> IN TRANSITION TO TOMBSTONE – 内存中 OLTP 引擎不需要这些 CFP，可以对它们进行垃圾收集。 此状态指示这些 CFP 在等待后台线程将它们转换为下一个状态（即 TOMBSTONE）。<br /><br /> TOMBSTONE – 这些 CFP 在等待文件流垃圾收集器进行垃圾收集。 ([sp_filestream_force_garbage_collection &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|文件中包含事务的下限。 如果状态列不是 2、3 或 4，则为 Null。|  
|upper_bound_tsn|**bigint**|文件中包含事务的上限。 如果状态列不是 2、3 或 4，则为 Null。|  
|last_backup_page_count|**int**|上次备份时确定的逻辑页计数。 状态列设置为 2、3、4 或 5 时应用。 如果页计数未知，则为 NULL。|  
|delta_watermark_tsn|**int**|写入此差异文件的上个检查点的事务。 这是差异文件的水印。|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|仍需要文件的上个检查点的恢复日志序列号。|  
|tombstone_operation_lsn|**nvarchar(23)**|tombstone_operation_lsn 落后于日志截断日志序列号之后，文件将删除。|  
|logical_deletion_log_block_id|**bigint**|仅适用于状态 5。|  
  
## <a name="permissions"></a>Permissions  
 要求具有对服务器的 `VIEW DATABASE STATE` 权限。  
  
## <a name="use-cases"></a>用例  
 您可以评估，如下所示使用内存中 OLTP 的存储：  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
若要查看通过运行以下查询的状态和文件类型的存储使用量的细目分类：
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>请参阅  
 [内存优化表动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
