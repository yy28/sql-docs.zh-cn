---
title: "sys.resource_usage （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs: TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
caps.latest.revision: "15"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48a5b1046abf347c5a1239bbcd07c96da4476d98
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourceusage-azure-sql-database"></a>sys.resource_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  此功能处于预览状态。 请不要依赖于此功能的特定实现，因为此功能在将来的版本中可能更改或删除。  
>   
>  当处于预览状态时，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 运营团队可能针对此 DMV 打开和关闭数据集合：  
>   
>  -   如果打开，DMV 在聚合时将返回当前数据。  
> -   如果关闭，则 DMV 返回历史数据，这些数据可能是旧数据。  
  
 为当前服务器中的用户数据库提供资源使用情况数据的每小时摘要。 历史数据将保留 90 天。  
  
 对于每个用户数据库，以连续方式为每小时提供一行信息。 即使数据库在该小时内处于闲置状态，也有对应的一行，并且该数据库的 usage_in_seconds 值将为 0。 将相应地为该小时累积存储使用情况和 SKU 信息。  
  
|列|数据类型|Description|  
|-------------|---------------|-----------------|  
|time|**datetime**|时间 (UTC)（以小时增量表示）。|  
|database_name|**nvarchar**|用户数据库的名称。|  
|sku|**nvarchar**|SKU 的名称。 下面是可能的值：<br /><br /> Web<br /><br /> Business<br /><br /> 基本<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|该小时内使用的 CPU 时间之和。<br /><br /> 注意： 此列已弃用的 V11 并不适用于 V12。 **值始终设置为 0。**|  
|storage_in_megabytes|**decimal**|该小时的最大存储大小，包括数据库数据、索引、存储过程和元数据。|  
  
## <a name="permissions"></a>Permissions  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
  
