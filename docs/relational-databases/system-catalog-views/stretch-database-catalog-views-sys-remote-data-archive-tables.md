---
title: sys.remote_data_archive_tables (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 93dfc97acab31b5078bcba569b52c64f773c775b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945672"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch Database 目录视图的 sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含每个远程表，用于存储已启用延伸的本地表中的数据行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|已启用延伸的本地表对象 ID。|  
|**remote_database_id**|**int**|自动生成本地标识符的远程数据库。|  
|**remote_table_name**|**sysname**|对应于已启用延伸的本地表的远程数据库中的表的名称。|  
|**filter_predicate**|**nvarchar(max)**|如果任何的筛选器谓词，用于标识要迁移的表中的行。 如果值为 null，则整个表都可迁移。<br /><br /> 有关详细信息，请参阅[为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)并[选择要迁移使用筛选器谓词的行](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。|  
|**migration_direction**|**tinyint**|当前正在中迁移数据的方向。 可用值如下所示。<br/>1 （出站）<br/>2 （入站）|  
|**migration_direction_desc**|**nvarchar(60)**|当前正在中迁移数据的方向的说明。 可用值如下所示。<br/>出站 (1)<br/>入站 (2)|  
|**is_migration_paused**|**bit**|指示是否当前已暂停迁移。|  
|**is_reconciled**|**bit**| 指示是否同步对远程表和 SQL Server 表。<br/><br/>时的值**is_reconciled**为 1 (true)、 远程表和 SQL Server 表保持同步，并且可以运行包含远程数据的查询。<br/><br/>时的值**is_reconciled**为 0 (false)，则在远程表和 SQL Server 表不同步。最近已迁移的行必须再次迁移。 还原远程 Azure 数据库，或删除行手动从远程表时，将发生这种情况。 直到您对帐表，不能运行包含远程数据的查询。 若要对帐表，请运行[sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)。 |  
  
## <a name="see-also"></a>请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  

