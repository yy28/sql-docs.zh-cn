---
title: catalog.environments（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2bc933212c4e8f7dfe6f29aeb386b65874e3d91b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038381"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有环境的环境详细信息。 环境包含可由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目引用的变量。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|环境的唯一标识符 (ID)。|  
|NAME|**sysname**|环境的名称。|  
|folder_id|**bigint**|环境位于其中的文件夹的唯一 ID。|  
|description|**nvarchar(1024)**|环境的说明。 该值是可选的。|  
|created_by_sid|**varbinary(85)**|创建了环境的用户的安全标识符 (SID)。|  
|created_by_name|**nvarchar(128)**|创建环境的用户名。|  
|created_time|**datetimeoffset**|创建环境的日期和时间。|  
  
## <a name="remarks"></a>Remarks  
 此视图对于目录中的每个环境显示一行。 环境名称只是相对于它们所在的文件夹是唯一的。 例如，名为 `E1` 的环境可能存在于目录中的多个文件夹中，但每个文件夹只能有一个名为 `E1` 的环境。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对环境的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  将实施行级安全性；只显示您有权查看的行。  
  
  
