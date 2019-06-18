---
title: MSdbms_map (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad9106bb9cde64953643e86bf81e72684858bd65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62817113"
---
# <a name="msdbmsmap-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_map**表包含源数据类型信息，以及源和目标 DBMS 对的默认目标数据类型信息的链接。 此表存储中**msdb**数据库和用于异类发布。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|唯一标识数据类型映射。|  
|**src_dbms_id**|**int**|通过指定标识源 DBMS 及其**dbms_id**中[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)表。|  
|**dest_dbms_id**|**int**|通过指定标识目标 DBMS 及其**dbms_id**中[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)表。|  
|**src_datatype_id**|**int**|标识**datatype_id**从[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)源数据类型的表。|  
|**src_len_min**|**bigint**|源 DBMS 中的数据类型的最小长度，值为 NULL 表示不使用该长度。|  
|**src_len_max**|**bigint**|源 DBMS 中的数据类型的最大长度，值为 NULL 表示不使用该长度。|  
|**src_prec_min**|**bigint**|源 DBMS 中的数据类型的最小精度，值为 NULL 表示不使用该精度。|  
|**src_prec_max**|**bigint**|源 DBMS 中的数据类型的最大精度，值为 NULL 表示不使用该精度。|  
|**src_scale_min**|**int**|源 DBMS 中的数据类型的最小小数位数，值为 NULL 表示不使用该小数位数。|  
|**src_scale_max**|**int**|源 DBMS 中的数据类型的最大小数位数，值为 NULL 表示不使用该小数位数。|  
|**src_nullable**|**bit**|指示映射中的目标列是否允许 NULL 值，其中 NULL 值意味着此定义不是必需的。|  
|**default_datatype_mapping_id**|**int**|通过指定标识的默认数据类型映射及其**map_id**表中[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
