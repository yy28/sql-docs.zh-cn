---
title: "dbo.slo_service_objectives （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a5d3a911aa1ffa5088f2a817c2434c98eb7cbe3
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2018
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  此功能处于预览状态，并且未弃用[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V12。 请不要依赖于此功能的特定实现，因为此功能在将来的版本中可能更改或删除。  
  
 返回有关当前服务器的服务级别目标 (SLO) 信息。  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|服务级别目标的 ID。|  
|name|**sysname**|服务级别目标的名称。|  
|description|**nvarchar**|服务级别目标的说明。|  
|create_date|**datetimeoffset(7)**|服务器上服务级别目标的创建日期。|  
|is_system|**bit**|1 = 系统服务级别目标|  
|is_default|**bit**|1 = 服务级别目标为默认 SLO。|  
|state|**tinyint**|1 = 服务级别目标启用。<br /><br /> 2 = 服务级别目标禁用。|  
|state_desc|**nvarchar**|服务级别目标的说明。|  
|metadata_version|**decimal**|服务级别目标的版本。|  
  
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="see-also"></a>另请参阅  
 [管理高级数据库](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
