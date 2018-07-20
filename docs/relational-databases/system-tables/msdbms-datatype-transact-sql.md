---
title: MSdbms_datatype (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10e748d771414e9dee552a0e0f7ecdc643ba298a
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103535"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype**表包含在用作发布服务器或订阅服务器在异类数据库复制每个受支持的数据库管理系统 (DBMS) 的本机数据类型的完整列表。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|标识每个唯一的数据类型。|  
|**dbms_id**|**int**|标识数据类型所属的 DBMS。|  
|**类型**|**sysname**|数据类型名称（本机）。|  
|**createparams**|**int**|说明哪一长度、精度和小数位数组合适用于每种数据类型的位图，包括：<br /><br /> **0x1** = 精度。<br /><br /> **0x2** = 规模。<br /><br /> **0x4** = 长度。|  
  
## <a name="remarks"></a>Remarks  
 此表包含 SQL Server 数据类型的条目，因为 SQL Server 的实例可以同时订阅非 SQL Server 数据库和发布到非 SQL Server 订阅服务器。  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 发布服务器的数据类型映射](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
