---
title: sys.remote_data_archive_tables (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19ae2040d65a7e7c8a36cef8f355e8715283c92d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>拉伸数据库目录视图-sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含有关将数据从已启用延伸的本地表存储每个远程表的一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|已启用延伸的本地表对象 ID。|  
|**remote_database_id**|**int**|自动生成本地标识符的远程数据库。|  
|**remote_table_name**|**sysname**|对应于已启用延伸的本地表的远程数据库中的表的名称。|  
|**filter_predicate**|**nvarchar(max)**|筛选器谓词中，如果有的话，识别要迁移的表中的行。 如果值为 null，则整个表都可迁移。<br /><br /> 有关详细信息，请参阅[为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[选择要迁移通过使用筛选器谓词的行](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。|  
|**migration_direction**|**tinyint**|当前正在顺序迁移数据的方向。 可用值如下所示。<br/>1 （出站）<br/>2 （入站）|  
|**migration_direction_desc**|**nvarchar(60)**|当前正在顺序迁移数据的方向的说明。 可用值如下所示。<br/>出站 (1)<br/>入站 (2)|  
|**is_migration_paused**|**bit**|指示是否迁移当前已暂停。|  
|**is_reconciled**|**bit**| 指示是否同步远程表和 SQL Server 表。<br/><br/>时的值**is_reconciled**为 1 (true)、 远程表和 SQL Server 表的同步，并且你可以运行包含远程数据查询。<br/><br/>时的值**is_reconciled**为 0 (false)、 远程表和 SQL Server 表不同步。最近已迁移的行必须再次迁移。 当还原远程 Azure 数据库，或者当你行手动删除远程表中，将发生这种情况。 直到你先对帐表，不能运行包含远程数据查询。 若要先对帐表，运行[sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)。 |  
  
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  

