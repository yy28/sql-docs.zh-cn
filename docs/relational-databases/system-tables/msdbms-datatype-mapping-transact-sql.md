---
title: MSdbms_datatype_mapping (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d513da9588b8ae8fb4f20ece11390c29d71bcf9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750091"
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype_mapping**表包含从数据类型的允许的数据类型映射到目标 DBMS 中的一个或多个特定的数据类型源数据库管理系统 (DBMS) 中。 此表存储中**msdb**数据库，用于异类数据库复制。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|标识每个唯一的数据类型映射。|  
|**map_id**|**int**|标识源数据类型。|  
|**dest_datatype_id**|**int**|标识目标数据类型。|  
|**dest_precision**|**bigint**|定义目标数据类型，其中的值为 NULL 表示不使用精度，精度的值**为-1**表明使用源数据类型的精度。|  
|**dest_scale**|**int**|定义目标数据类型，其中的值为 NULL 表示不使用小数位数，小数位数的值**为-1**表明使用源数据类型的小数位数。|  
|**dest_length**|**bigint**|定义目标数据类型，其中的值为 NULL 表示不使用长度，长度的值**为-1**表明使用源数据类型的长度。|  
|**dest_nullable**|**bit**|指示映射中的目标列是否允许 NULL 值，其中 NULL 值意味着此定义不是必需的。|  
|**dest_createparams**|**int**|位图，用于说明适用于每种数据类型的长度、精度和小数位数组合，其中包括：<br /><br /> **0x1** = 精度。<br /><br /> **0x2** = 规模。<br /><br /> **0x4** = 长度。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
