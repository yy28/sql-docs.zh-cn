---
title: "dbo.slo_assignment_history （Azure SQL 数据库） |Microsoft 文档"
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
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61bab47646d1acff9edcfbf461588b3560916acd
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2018
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **这仅适用于[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
>   
>  此功能处于预览状态。 请不要依赖于此功能的特定实现，因为此功能在将来的版本中可能更改或删除。  
  
 返回服务器中数据库 SLO 分配的历史记录，包括：  
  
-   服务器中数据库 SLO 分配的历史记录。  
  
-   每个数据库 SLO 更改请求的开始时间和结束时间。  
  
-   在 error_code 和 error_desc 列中记录的所有 SLO 分配错误。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|数据库的名称。|  
|database_id|**int**|数据库 ID。|  
|create_date|**datetimeoffset(7)**|数据库的创建日期。|  
|service_objective_name|**sysname**|服务级别目标 (SLO) 的名称。|  
|service_objective_id|**uniqueidentifier**|SLO 的 ID。|  
|operation_id|**uniqueidentifier**|操作的 ID。|  
|operation_start_time|**datetimeoffset(7)**|数据库 SLO 更改请求的开始时间。|  
|operation_end_time|**datetimeoffset(7)**|数据库 SLO 更改请求的结束时间。|  
|error_code|**int**|数据库 SLO 更改请求的错误代码。|  
|error_desc|**nvarchar**|数据库 SLO 更改请求中错误的说明。|  
  
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="examples"></a>示例  
 以下示例返回指定数据库的数据库 SLO 分配历史记录。  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [管理高级数据库](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
