---
title: sys.dm_resource_governor_configuration (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_resource_governor_configuration_TSQL
- dm_resource_governor_configuration
- sys.dm_resource_governor_configuration
- sys.dm_resource_governor_configuration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_configuration dynamic management view
ms.assetid: c89aab6a-0434-4ce6-af8c-f8a1a3284e38
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be759922c1ebf957d26a81f346c1ddb0a8dcd2a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmresourcegovernorconfiguration-transact-sql"></a>sys.dm_resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回包含资源调控器的当前内存中配置状态的行。  
  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|资源调控器当前使用的分类器函数的 ID。 如果没有正在使用的函数，则返回值 0。 不可为 null。<br /><br /> **注意：**此函数可用于将新请求，并使用规则来将这些请求路由到相应的工作负荷组。 有关详细信息，请参阅 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。|  
|is_reconfiguration_pending|**bit**|指示是否由 ALTER RESOURCE GOVERNOR RECONFIGURE 语句对组或池进行了更改但尚未应用到内存中配置。 返回值是以下值之一：<br /><br /> 0 - 不需要重新配置语句。<br /><br /> 1 - 需要重新配置语句或重新启动服务器，以便应用挂起的配置更改。<br /><br /> **注意：**返回的值始终为 0 时禁用资源调控器。<br /><br /> 不可为 null。|  
|max_outstanding_io_per_volume|**int**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 每个卷待定 I/O 的最大数目。|  
  
## <a name="remarks"></a>注释  
 此动态管理视图显示了内存中配置。 若要查看存储的配置元数据，请使用对应的目录视图。  
  
 下面的示例演示了如何获取和比较存储的元数据值和资源调控器配置的内存中值。  
  
```  
USE master;  
go  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
go  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
go  
```  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.resource_governor_configuration &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)  
  
  

