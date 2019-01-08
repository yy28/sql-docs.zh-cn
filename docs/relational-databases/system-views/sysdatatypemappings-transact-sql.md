---
title: sysdatatypemappings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31f90836b26d9551cc3e5a1200208cc51e3ef30a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756939"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysdatatypemappings**视图用于显示 SQL Server 数据类型和数据类型的非 SQL Server 数据库管理系统 (DBMS) 之间的映射。 此视图存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|数据类型映射的 ID。|  
|**source_dbms**|**sysname**|指示从中映射数据类型的 DBMS 的名称，可以是下列值之一：<br /><br /> **MSSQLSERVER** = 源是 SQL Server 数据库。<br /><br /> **ORACLE** = 源数据库为 Oracle 数据库。|  
|**source_version**|**sysname**|指示源 DBMS 的产品版本。|  
|**source_type**|**sysname**|指示在源 DBMS 中列出的数据类型。|  
|**source_length_min**|**bigint**|源 DBMS 中的数据类型的最小长度，值为 NULL 表示不使用该长度。|  
|**source_length_max**|**bigint**|源 DBMS 中的数据类型的最大长度，值为 NULL 表示不使用该长度。|  
|**source_precision_min**|**bigint**|源 DBMS 中的数据类型的最小精度，值为 NULL 表示不使用该精度。|  
|**source_precision_max**|**bigint**|源 DBMS 中的数据类型的最大精度，值为 NULL 表示不使用该精度。|  
|**source_scale_min**|**int**|源 DBMS 中的数据类型的最小小数位数，值为 NULL 表示不使用该小数位数。|  
|**source_scale_max**|**int**|源 DBMS 中的数据类型的最大小数位数，值为 NULL 表示不使用该小数位数。|  
|**source_nullable**|**bit**|指示目标数据类型是否支持 Null 值。|  
|**source_createparams**|**int**|仅限内部使用。|  
|**destination_dbms**|**sysname**|指示目标 DBMS 的名称，可以是下列值之一：<br /><br /> **MSSQLSERVER** = 目标数据库为 SQL Server 数据库。<br /><br /> **ORACLE** = 目标数据库为 Oracle 数据库。<br /><br /> **DB2** = 目标数据库为 IBM DB2 数据库。<br /><br /> **SYBASE** = 目标数据库为 Sybase 数据库。|  
|**destination_version**|**sysname**|目标 DBMS 的产品版本。|  
|**destination_type**|**sysname**|目标 DBMS 中的数据类型。|  
|**destination_length**|**bigint**|目标 DBMS 中的数据类型的长度。|  
|**destination_precision**|**bigint**|目标 DBMS 中的数据类型的精度。|  
|**destination_scale**|**int**|目标 DBMS 中的数据类型的小数位数。|  
|**destination_nullable**|**bit**|指示目标 DBMS 中的数据类型是否支持 Null 值。|  
|**destination_createparams**|**int**|仅限内部使用。|  
|**数据丢失**|**bit**|指示在源和目标 DBMS 中的数据类型之间映射时是否发生数据丢失。|  
|**is_default**|**bit**|指示默认情况下是否使用数据类型映射。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
