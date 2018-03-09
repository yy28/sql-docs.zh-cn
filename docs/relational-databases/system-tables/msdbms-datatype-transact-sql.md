---
title: "MSdbms_datatype (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd690436908a61b43b4e7af829e8bc3528fd5305
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype**表包含在作为发布服务器或订阅服务器中异类数据库复制使用每个受支持的数据库管理系统 (DBMS) 的本机数据类型的完整列表。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|标识每个唯一的数据类型。|  
|**dbms_id**|**int**|标识数据类型所属的 DBMS。|  
|**type**|**sysname**|数据类型名称（本机）。|  
|**createparams**|**int**|说明哪一长度、精度和小数位数组合适用于每种数据类型的位图，包括：<br /><br /> **0x1** = 精度。<br /><br /> **0x2** = SCALE。<br /><br /> **0x4** = LENGTH。|  
  
## <a name="remarks"></a>注释  
 此表包含 SQL Server 数据类型的条目，因为 SQL Server 的实例可以订阅非 SQL Server 数据库和发布到非 SQL Server 订阅服务器。  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
