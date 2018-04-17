---
title: sysmergepartitioninfo (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d656ae83e03c3fc17ec71335055db7ddb677649d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有关每个项目的分区的信息。 本地数据库中定义的每个合并项目都在表中占一行。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**pubid**|**uniqueidentifier**|此发布的唯一标识号；在添加发布时生成。|  
|**partition_view_id**|**int**|该表的分区视图 ID。 该视图显示项目中每行到它所属的不同分区 ID 的映射。|  
|**repl_view_id**|**int**|内容待定。|  
|**partition_deleted_view_rule**|**nvarchar(4000)**|在合并复制触发器内部使用的 SQL 语句，用于根据其旧列值检索每个已删除或已更新行的分区 ID。|  
|**partition_inserted_view_rule**|**nvarchar(4000)**|在合并复制触发器内部使用的 SQL 语句，用于根据其新列值检索每个已插入或已更新行的分区 ID。|  
|**membership_eval_proc_name**|**sysname**|中的行的当前分区 Id 的计算结果的过程的名称**MSmerge_contents**。|  
|**column_list**|**nvarchar(4000)**|在项目中复制的列的逗号分隔列表。|  
|**column_list_blob**|**nvarchar(4000)**|在项目中复制的列（包括二进制大型对象列）的逗号分隔列表。|  
|**expand_proc**|**sysname**|过程名称，该过程重新计算新插入的父行的所有子行的分区 ID，以及经历了分区更改或已被删除的父行的分区 ID。|  
|**logical_record_parent_nickname**|**int**|逻辑记录中指定项目的顶级父项目的别名。|  
|**logical_record_view**|**int**|一个视图，用于输出与各子项目 rowguid 相对应的顶级父项目 rowguid。|  
|**logical_record_deleted_view_rule**|**nvarchar(4000)**|类似于**logical_record_view**，但它显示的是"已删除"表中的子行更新和删除触发器。|  
|**logical_record_level_conflict_detection**|**bit**|指示应在逻辑记录级还是行级或列级检测冲突。<br /><br /> **0** = 行或列级别使用冲突检测。<br /><br /> **1** = 逻辑记录冲突检测时，在发布服务器上的行中的更改和更改在单独的行的同一逻辑订阅服务器上的记录会被视为冲突。<br /><br /> 当此值是**1**，可以使用仅逻辑记录级冲突解决方法。|  
|**logical_record_level_conflict_resolution**|**bit**|指示应在逻辑记录级别还是行或列级别解决冲突。<br /><br /> **0** = 行或列级别使用解析。<br /><br /> **1** = 以防中入选方的整个逻辑记录的冲突时，将覆盖落选方上的整个逻辑记录。<br /><br /> 值为**1**可用来使用这两个逻辑记录级检测，并且使用行级或列级检测。|  
|**partition_options**|**tinyint**|定义项目数据的分区方式，当所有行只属于一个分区或只属于一个订阅时，这将可以实现性能优化。 *partition_options*可以是以下值之一。<br /><br /> **0** = 筛选的项目是静态的或不会生成唯一的每个分区，即"重叠"分区的数据子集。<br /><br /> **1** = 分区重叠，并且订阅服务器上所做的 DML 更新不能更改行属于哪个分区。<br /><br /> **2** = 筛选文章生成不重叠分区，但多个订阅服务器可以接收相同的分区。<br /><br /> **3** = 筛选的项目生成对每个订阅都是唯一的不重叠分区。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
