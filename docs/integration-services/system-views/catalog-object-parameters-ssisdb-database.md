---
title: "catalog.object_parameters （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d538e5b55ef4e8880afb2d008b11c17d9a03189
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有包和项目的参数。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|参数的唯一标识符 (ID)。|  
|project_id|**bigint**|项目的唯一 ID。|  
|object_type|**int**|参数的类型。 对于项目参数，该值是 `20`；对于包参数，值是 `30`。|  
|object_name|**sysname**|包含对应项目或包的名称。|  
|parameter_name|**sysname(nvarchar(128))**|参数名。|  
|data_type|**nvarchar （128)**|参数的数据类型。|  
|required|**bit**|如果值为 `1`，则需要参数值才能开始执行。 如果值为 `0`，则不需要参数值即可开始执行。|  
|sensitive|**bit**|当值为 `1` 时，参数值是敏感的。 当值为 `0` 时，参数值是不敏感的。|  
|description|**nvarchar(1024)**|包的可选描述。|  
|design_default_value|**sql_variant**|在设计项目或包的过程中分配的参数的默认值。|  
|default_value|**sql_variant**|服务器上当前使用的默认值。|  
|value_type|**char （1)**|指示参数值的类型。 此字段将显示`V`parameter_value 时文字值和`R`当通过引用环境变量分配值。|  
|value_set|**bit**|如果值为 `1`，则已分配参数值。 如果值为 `0`，则尚未分配参数值。|  
|referenced_variable_name|**nvarchar （128)**|分配给参数值的环境变量的名称。 默认值是**NULL**。|  
|validation_status|**char （1)**|标识为仅供参考。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
|last_validation_time|**datetimeoffset(7)**|标识为仅供参考。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
  
## <a name="permissions"></a>Permissions  
 若要查看此视图中的行，您必须具有以下权限之一：  
  
-   针对项目的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   中的成员身份**sysadmin**服务器角色。  
  
 将实施行级安全性；只显示您有权查看的行。  
  
  

