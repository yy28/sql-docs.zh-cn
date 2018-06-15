---
title: sys.sysindexes (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
caps.latest.revision: 57
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 276d2bfd5374fc24b31648250b5ffcd1eefb1ac7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221998"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  当前数据库中的每个索引和表各对应一行。 此视图不支持 XML 索引。 已分区的表和索引不完全支持在此视图;使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)改用目录视图。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|索引所属表的 ID。|  
|**status**|**int**|系统状态信息。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|指向第一页或根页的指针。<br /><br /> 未使用的在**indid** = 0。<br /><br /> NULL = 索引进行分区时**indid** > 1。<br /><br /> NULL = 表进行分区时**indid**为 0 或 1。|  
|**indid**|**int**|索引 ID：<br /><br /> 0 = 堆<br /><br /> 1 = 聚集索引<br /><br /> > 1 = 非聚集索引|  
|**根**|**binary(6)**|有关**indid** > = 1，**根**是一个指针指向根页。<br /><br /> 未使用的在**indid** = 0。<br /><br /> NULL = 索引进行分区时**indid** > 1。<br /><br /> NULL = 表进行分区时**indid**为 0 或 1。|  
|**minlen**|**int**|行的最小大小。|  
|**keycnt**|**int**|键数。|  
|**groupid**|**int**|在其上创建对象的文件组 ID。<br /><br /> NULL = 索引进行分区时**indid** > 1。<br /><br /> NULL = 表进行分区时**indid**为 0 或 1。|  
|**dpages**|**int**|有关**indid** = 0 或**indid** = 1， **dpages**是使用的数据页的计数。<br /><br /> 有关**indid** > 1， **dpages**是使用的索引页的计数。<br /><br /> 0 = 索引进行分区时**indid** > 1。<br /><br /> 0 = 表进行分区时**indid**为 0 或 1。<br /><br /> 如果发生行溢出，则不会得出准确的结果。|  
|**保留**|**int**|有关**indid** = 0 或**indid** = 1，**保留**是分配的所有索引和表数据页的计数。<br /><br /> 有关**indid** > 1，**保留**是为索引分配的页数计数。<br /><br /> 0 = 索引进行分区时**indid** > 1。<br /><br /> 0 = 表进行分区时**indid**为 0 或 1。<br /><br /> 如果发生行溢出，则不会得出准确的结果。|  
|**used**|**int**|有关**indid** = 0 或**indid** = 1，**使用**是用于所有索引和表数据的总页数的计数。<br /><br /> 有关**indid** > 1，**使用**是用于索引的页的计数。<br /><br /> 0 = 索引进行分区时**indid** > 1。<br /><br /> 0 = 表进行分区时**indid**为 0 或 1。<br /><br /> 如果发生行溢出，则不会得出准确的结果。|  
|**rowcnt**|**bigint**|数据级别行计数基于**indid** = 0 和**indid** = 1。<br /><br /> 0 = 索引进行分区时**indid** > 1。<br /><br /> 0 = 表进行分区时**indid**为 0 或 1。|  
|**rowmodctr**|**int**|对自上次更新表的统计信息后插入、删除或更新行的总数进行计数。<br /><br /> 0 = 索引进行分区时**indid** > 1。<br /><br /> 0 = 表进行分区时**indid**为 0 或 1。<br /><br /> 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本， **rowmodctr**不是与早期版本完全兼容。 有关详细信息，请参阅“备注”。|  
|**reserved3**|**int**|返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**int**|最大行大小|  
|**maxirow**|**int**|最大非叶索引行大小。<br /><br /> 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本， **maxirow**不是与早期版本完全兼容。|  
|**OrigFillFactor**|**tinyint**|创建索引时使用的初始填充因子值。 不保留该值；但如果需要重新创建索引但不记得当初使用的填充因子，则该值可能很有帮助。|  
|**StatVersion**|**tinyint**|返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = 索引已分区。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**int**|索引实现标志。<br /><br /> 返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**int**|用于约束经过考虑的索引锁粒度。 例如，对于本质上是只读的查找表，可以将其设置为仅进行表级锁定以最大限度地降低锁定成本。|  
|**pgmodctr**|**int**|返回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**密钥**|**varbinary(816)**|组成索引键的列 ID 列表。<br /><br /> 返回 NULL。<br /><br /> 若要显示的索引键列，请使用[sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md)。|  
|**名称**|**sysname**|索引或统计信息的名称。 时，则返回 NULL **indid** = 0。 修改应用程序以查找 NULL 堆名。|  
|**statblob**|**image**|统计信息二进制大型对象 (BLOB)。<br /><br /> 返回 NULL。|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**行**|**int**|数据级别行计数基于**indid** = 0 和**indid** = 1，并且值重复的**indid** > 1。|  
  
## <a name="remarks"></a>注释  
 不得使用定义为保留的列。  
  
 列**dpages**，**保留**，和**使用**如果表或索引包含 ROW_OVERFLOW 分配单元中的数据不会返回准确的结果。 此外，将单独跟踪每个索引的页计数，并且不对基表的页计数进行聚合。 若要查看页计数，请使用[sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)或[sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)目录视图，或[sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)动态管理视图。  
  
 在 SQL Server 2000 和更早期版本中，[!INCLUDE[ssDE](../../includes/ssde-md.md)]维护行级修改计数器。 现在，此类计数器在列级维护。 因此， **rowmodctr**列计算并生成类似于早期版本中的结果，但不精确的结果。  
  
 如果使用中的值**rowmodctr**若要确定何时更新统计信息，请考虑以下解决方案：  
  
-   不执行任何操作。 新**rowmodctr**值经常将帮助你确定何时更新统计信息，因为行为规范的合理接近早期版本的结果。  
  
-   使用 AUTO_UPDATE_STATISTICS。 有关详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
-   使用时间限制确定更新统计信息的时间。 例如，每小时、每天或每周。  
  
-   使用应用程序级信息确定更新统计信息的时间。 例如，每次的最大值**标识**列通过多个 10000，来更改或执行每次在大容量插入操作。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [将系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
