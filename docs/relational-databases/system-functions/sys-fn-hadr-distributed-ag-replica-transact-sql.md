---
title: sys.fn_hadr_distributed_ag_replica (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 883df7cb9358d0791d9ea3af520a52d3a480da4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821542"
---
# <a name="sysfnhadrdistributedagreplica-transact-sql"></a>sys.fn_hadr_distributed_ag_replica (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  用于将分布式的可用性组中的副本映射到本地可用性组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>参数  
 '*lag_Id*'  
 是分布式的可用性组的标识符。 *lag_Id*是类型**uniqueidentifier**。  
  
 '*replica_id*  
 是分布式的可用性组中的标识符。 *replica_id*是类型**uniqueidentifier**。  
  
## <a name="tables-returned"></a>返回的表  
 返回以下信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|本地可用性组的唯一标识符 (GUID)。|  
  
## <a name="examples"></a>示例  
  
### <a name="using-sysfnhadrdistributedagreplica"></a>使用 sys.fn_hadr_distributed_ag_replica  
 下面的示例返回与指定的分布式的可用性组和副本相关联的本地可用性组标识符包含的表。  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组函数&#40;Transact SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性组&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [分布式可用性组&#40;AlwaysOn 可用性组&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
