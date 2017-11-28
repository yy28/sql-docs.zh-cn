---
title: "sys.allocation_units (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.allocation_units_TSQL
- sys.allocation_units
- allocation_units_TSQL
- allocation_units
dev_langs: TSQL
helpviewer_keywords: sys.allocation_units catalog view
ms.assetid: ec9de780-68fd-4551-b70b-2d3ab3709b3e
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5b689c65c59357ff4910701051125e4bd58361ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysallocationunits-transact-sql"></a>sys.allocation_units (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  数据库中的每个分配单元都在表中占一行。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|分配单元的 ID。 是一个数据库中唯一的。|  
|类型|**tinyint**|分配单元的类型：<br /><br /> 0 = 已删除<br /><br /> 1 = 行内数据（所有数据类型，但 LOB 数据类型除外）<br /><br /> 2 = 大型对象 (LOB) 数据 (**文本**， **ntext**，**映像**， **xml**，较大的值类型和 CLR 用户定义类型)<br /><br /> 3 = 行溢出数据|  
|type_desc|**nvarchar(60)**|对分配单元类型的说明：<br /><br /> **删除**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|与分配单元关联的存储容器的 ID。<br /><br /> 如果 type = 1 或 3，则 container_id = sys.partitions.hobt_id。<br /><br /> 如果 type 为 2，则 container_id = sys.partitions.partition_id。<br /><br /> 0 = 标记为要延迟删除的分配单元|  
|data_space_id|**int**|此分配单元所在文件组的 ID。|  
|total_pages|**bigint**|此分配单元分配或保留的总页数。|  
|used_pages|**bigint**|实际使用的总页数。|  
|data_pages|**bigint**|包含下列数据的已使用页的数目：<br /><br /> 行内数据<br /><br /> LOB 数据<br /><br /> 行溢出数据<br /><br /> <br /><br /> 请注意，返回的值不包括内部索引页和分配管理页。|  
  
> [!NOTE]  
>  在删除或重新生成大型索引时，或者在删除或截断大型表时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将延迟实际页释放及其关联锁，直至事务提交完毕为止。 延迟的删除操作不会立即释放已分配的空间。 因此，删除或截断大型对象之后立即由 sys.allocation_units 返回的值可能不会反映实际可用的磁盘空间。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.partitions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
