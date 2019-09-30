---
title: catalog.environment_references（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 848e337ecfacd16df1b34a60e392b572b612735d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295201"
---
# <a name="catalogenvironment_references-ssisdb-database"></a>catalog.environment_references（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 **SSISDB** 目录中所有项目的环境引用。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|引用的唯一标识符 (ID)。|  
|project_id|**bigint**|项目的唯一 ID。|  
|reference_type|**char(1)**|指示环境是可以位于与项目相同的文件夹中（相对引用），还是位于其他文件夹中（绝对引用）中。 如果值为 `R`，则通过使用相对引用定位环境。 如果值为 `A`，则通过使用绝对引用定位环境。|  
|environment_folder_name|**sysname**|如果环境是通过使用绝对引用定位的，则为文件夹的名称。|  
|environment_name|**sysname**|项目引用的环境的名称。|  
|validation_status|**char(1)**|验证的状态。|  
|last_validation_time|**datatimeoffset(7)**|最后验证的时间。|  
  
## <a name="remarks"></a>Remarks  
 此视图对于目录中的每个环境引用显示一行。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对相应项目的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格。  
  
> [!NOTE]  
>  如果您对项目具有 READ 权限，则也对与该项目关联的所有包和环境引用具有 READ 权限。 将实施行级安全性；只显示您有权查看的行。  
  
## <a name="remarks"></a>Remarks  
 项目可以具有相对或绝对的环境引用。 相对引用通过名称引用环境，并要求它与项目位于相同文件夹中。 绝对引用通过名称和文件夹引用环境，可能引用与项目不在同一文件夹中的环境。 项目可以引用多个环境。  
  
  
