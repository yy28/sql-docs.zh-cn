---
title: MSdbms （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_TSQL
- MSdbms
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms system table
ms.assetid: 2be631bf-de09-4e7a-9ccb-d6c37b81c237
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2cd44c5154668513d695071c23619e650497c8a8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907487"
---
# <a name="msdbms-transact-sql"></a>MSdbms (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms**表包含异类数据库复制所支持的所有版本的数据库管理系统（DBMS）的主列表。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**dbms_id**|**int**|标识每个唯一的 DBMS 和版本。|  
|**而言**|**sysname**|DBMS 名称。<br /><br /> MSSQLSERVER<br /><br /> DB2<br /><br /> ORACLE<br /><br /> SYBASE|  
|**version**|**varchar （10）**|DBMS 版本。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
