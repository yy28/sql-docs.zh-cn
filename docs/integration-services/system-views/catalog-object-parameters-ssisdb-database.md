---
title: "catalog.object_parameters（SSISDB 数据库）| Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c154da24447377cb9f2602a46a116364336e1c1e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有包和项目的参数。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|参数的唯一标识符 (ID)。|  
|project_id|**bigint**|项目的唯一 ID。|  
|object_type|**int**|参数的类型。 对于项目参数，该值是 `20`；对于包参数，值是 `30`。|  
|object_name|**sysname**|包含对应项目或包的名称。|  
|parameter_name|**sysname(nvarchar(128))**|参数名。|  
|data_type|**nvarchar(128)**|参数的数据类型。|  
|required|**bit**|如果值为 `1`，则需要参数值才能开始执行。 如果值为 `0`，则不需要参数值即可开始执行。|  
|sensitive|**bit**|当值为 `1` 时，参数值是敏感的。 当值为 `0` 时，参数值是不敏感的。|  
|description|**nvarchar(1024)**|包的可选说明。|  
|design_default_value|**sql_variant**|在设计项目或包的过程中分配的参数的默认值。|  
|default_value|**sql_variant**|服务器上当前使用的默认值。|  
|value_type|**char(1)**|指示参数值的类型。 当 parameter_value 为文本值时，此字段显示 `V`；当该值通过引用环境对象来分配时，此字段显示 `R`。|  
|value_set|**bit**|如果值为 `1`，则已分配参数值。 如果值为 `0`，则尚未分配参数值。|  
|referenced_variable_name|**nvarchar(128)**|分配给参数值的环境变量的名称。 默认值为 NULL。|  
|validation_status|**char(1)**|标识为仅供参考。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
|last_validation_time|**datetimeoffset(7)**|标识为仅供参考。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
  
## <a name="permissions"></a>权限  
 若要查看此视图中的行，您必须具有以下权限之一：  
  
-   针对项目的 READ 权限  
  
-   ssis_admin 数据库角色的成员资格  
  
-   sysadmin 服务器角色中的成员资格。  
  
 将实施行级安全性；只显示您有权查看的行。  
  
  
