---
title: MSdbms_datatype （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
ms.openlocfilehash: 301aa5af9aa34031f381235341f1e7d461675432
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907513"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype**表包含在异类数据库复制中用作发布服务器或订阅服务器的每个受支持的数据库管理系统（DBMS）的本机数据类型的完整列表。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|标识每个唯一的数据类型。|  
|**dbms_id**|**int**|标识数据类型所属的 DBMS。|  
|type |**sysname**|数据类型名称（本机）。|  
|**createparams**|**int**|说明哪一长度、精度和小数位数组合适用于每种数据类型的位图，包括：<br /><br /> **0x1** = 精度。<br /><br /> **0x2** = SCALE。<br /><br /> **0x4** = LENGTH。|  
  
## <a name="remarks"></a>备注  
 此表包含 SQL Server 数据类型项，因为 SQL Server 实例既可以订阅非 SQL Server 数据库，也可以发布到非 SQL Server 订阅服务器。  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
