---
title: sys. fn_hadr_distributed_ag_database_replica （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7b894919a4149d37181d543b8d58fc820aad10b
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052992"
---
# <a name="sysfn_hadr_distributed_ag_database_replica-transact-sql"></a>sys. fn_hadr_distributed_ag_database_replica （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  用于将分布式可用性组中的数据库映射到本地可用性组中的数据库。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>自变量  
 "*lag_Id*"  
 是分布式可用性组的标识符。 *lag_Id*为类型**uniqueidentifier**。  
  
 "*database_id*"  
 是分布式可用性组中的数据库的标识符。 *database_id*为类型**uniqueidentifier**。  
  
## <a name="tables-returned"></a>返回的表  
 返回以下信息。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|本地可用性组中的数据库的 ID。|  
  
## <a name="examples"></a>示例  
  
### <a name="using-sysfn_hadr_distributed_ag_database_replica"></a>使用 sys. fn_hadr_distributed_ag_database_replica  
 下面的示例传入了分布式可用性组中的数据库 ID。 它将返回一个表，其中包含与本地可用性组关联的数据库 ID。  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [Always On 可用性组函数 &#40;Transact-sql&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On 可用性组 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 可用性组 &#40;分布式可用性组&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
