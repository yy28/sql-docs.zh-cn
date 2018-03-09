---
title: sys.resource_governor_configuration (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_configuration_TSQL
- sys.resource_governor_configuration
- resource_governor_configuration_TSQL
- resource_governor_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_configuration catalog view
ms.assetid: 89099668-1dc6-4b07-9d8b-49bc95c7bfc0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35952ed1dd7d43261ed4672d8cd9161c02454138
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysresourcegovernorconfiguration-transact-sql"></a>sys.resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回存储的资源调控器状态。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|分类器函数存储在元数据中时的 ID。 不可为 null。<br /><br /> **请注意**此函数可用于将新的会话，并使用规则来将工作负荷路由到相应的工作负荷组。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。|  
|is_enabled|**bit**|指示资源调控器的当前状态：<br /><br /> 0 = 未启用资源调控器。<br /><br /> 1 = 启用资源调控器。<br /><br /> 不可为 null。|  
|max_outstanding_io_per_volume|**int**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 每个卷待定 I/O 的最大数目。|  
  
## <a name="remarks"></a>注释  
 该目录视图显示元数据中存储的资源调控器配置。 若要查看内存中的配置，请使用对应的动态管理视图。  
  
## <a name="permissions"></a>权限  
 若要查看内容，则需要拥有 VIEW ANY DEFINITION 权限；若要更改内容，则需要拥有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示了如何获取和比较存储的元数据值和资源调控器配置的内存中值。  
  
```  
USE master;  
GO  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
GO  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md)   
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)  
  
  
