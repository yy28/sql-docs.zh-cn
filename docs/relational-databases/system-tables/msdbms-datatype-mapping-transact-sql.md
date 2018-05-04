---
title: MSdbms_datatype_mapping (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3fa02d526bcd4042efa92032551d950b5f553932
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype_mapping**表包含从数据类型的允许的数据类型映射在源数据库管理系统 (DBMS) 到目标 DBMS 中的一个或多个特定的数据类型。 此表存储在**msdb**数据库和用于异类数据库复制。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|标识每个唯一的数据类型映射。|  
|**map_id**|**int**|标识源数据类型。|  
|**dest_datatype_id**|**int**|标识目标数据类型。|  
|**dest_precision**|**bigint**|定义目标数据类型，其中的值为 NULL 表示不使用精度，精度和的值 **-1**表示将使用的源数据类型的精度。|  
|**dest_scale**|**int**|定义目标数据类型，其中的值为 NULL 表示不使用小数位数的小数位数和的值 **-1**意味着，使用源数据类型的小数位数。|  
|**dest_length**|**bigint**|定义目标数据类型，其中的值为 NULL 表示不使用长度的长度和的值 **-1**意味着，使用源数据类型的长度。|  
|**dest_nullable**|**bit**|指示映射中的目标列是否允许 NULL 值，其中 NULL 值意味着此定义不是必需的。|  
|**dest_createparams**|**int**|位图，用于说明适用于每种数据类型的长度、精度和小数位数组合，其中包括：<br /><br /> **0x1** = 精度。<br /><br /> **0x2** = SCALE。<br /><br /> **0x4** = LENGTH。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
