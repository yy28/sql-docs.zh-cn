---
title: sys. pdw_nodes_tables （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5fa2412e61e30852497ffa00493ea6dbe244989a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001111"
---
# <a name="syspdw_nodes_tables-transact-sql"></a>sys. pdw_nodes_tables （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  主体拥有的每个表对象都包含一行，或对主体授予了某些权限。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|\<继承列>||有关此视图所继承的列的列表，请参阅[sys.databases](../system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。||  
|lob_data_space_id|**int**||始终为 0。|  
|filestream_data_space_id|**int**|FILESTREAM 文件组或的数据空间 ID[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|Null|  
|max_column_id_used|**int**|此表使用的最大列 ID。||  
|lock_on_bulk_load|**bit**|大容量加载期间将锁定表。|TBD|  
|uses_ansi_nulls|**bit**|在创建表时，将 SET ANSI_NULLS 数据库选项设置为 ON。|1|  
|is_replicated|**bit**|1 = 使用复制发布表。|0不支持复制。|  
|has_replication_filter|**bit**|1 = 表具有复制筛选器。|0|  
|is_merge_published|**bit**|1 = 使用合并复制发布表。|0不支持。|  
|is_sync_tran_subscribed|**bit**|1 = 使用立即更新订阅来订阅表。|0不支持。|  
|has_unchecked_assembly_data|**bit**|1 = 表包含依赖于上次 ALTER ASSEMBLY 期间定义发生更改的程序集的持久化数据。 在下一次成功执行 DBCC CHECKDB 或 DBCC CHECKTABLE 后将重置为 0。|0不支持 CLR。|  
|text_in_row_limit|**int**|0 = 未设置 Text in row 选项。|始终为 0。|  
|large_value_types_out_of_row|**bit**|1 = 在行外存储大值类型。|始终为 0。|  
|is_tracked_by_cdc|**bit**|1 = 已为表启用变更数据捕获|始终为 0;无 CDC 支持。|  
|lock_escalation|**tinyint**|表的 LOCK_ESCALATION 选项的值： 2 = 自动|始终为2。|  
|lock_escalation_desc|**nvarchar(60)**|Lock_escalation 选项的文本说明。|始终 "自动"。|  
|pdw_node_id|**int**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点的唯一标识符。|NOT NULL|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
