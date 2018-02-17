---
title: "dbo.slo_database_objectives （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_database_objectives
- dbo.slo_database_objectives_TSQL
- slo_database_objectives_TSQL
- slo_database_objectives
dev_langs:
- TSQL
helpviewer_keywords:
- slo_database_objectives
- dbo.slo_database_objectives
ms.assetid: a522569d-8cfc-4643-a170-1cd291e61eee
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10227990cb6c5928fcc403ee35a978cbf93ad6ca
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2018
---
# <a name="dboslodatabaseobjectives-azure-sql-database"></a>dbo.slo_database_objectives （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **这仅适用于[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
>   
>  有关 [！包括[ssSDSfull](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) （主机） 上操作 ALTER DATABASE。   
  
 返回 SQL 数据库中的服务级别目标 (SLO) 的分配状态。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|数据库的名称。|  
|current_slo|**sysname**|数据库的当前 SLO。|  
|target_slo|**sysname**|SLO 更改请求中指定的数据库的目标 SLO。|  
|state_desc|**nvarchar**|SLO 更改请求的状态：已完成或挂起。|  
  
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="examples"></a>示例  
  
```  
SELECT   
database_name=database_name.name   
    , current_slo=current_slo.name   
    , target_slo=target_slo.name   
    , state_desc=database_slo.state_desc   
FROM slo_database_objectives AS database_slo  
INNER JOIN slo_service_objectives AS current_slo ON database_slo.current_objective_id = current_slo.objective_id  
INNER JOIN slo_service_objectives AS target_slo ON database_slo.configured_objective_id = target_slo.objective_id  
INNER JOIN sys.databases AS database_name  ON database_slo.database_id = database_name.database_id;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [管理高级数据库](http://go.microsoft.com/fwlink/?LinkID=311927)  
[sys.dm_operation_status（Azure SQL 数据库）](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 
