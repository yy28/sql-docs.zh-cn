---
title: "catalog.packages （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- packages view [Integration Services]
- catalog.packages view [Integration Services]
ms.assetid: a634e94d-f492-4dfd-9611-a35f545106a1
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f836c2b1bdf59f157f10abb708ed55f99dfc9f0f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogpackages-ssisdb-database"></a>catalog.packages（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示中显示的所有包的详细信息**SSISDB**目录。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|package_id|**bigint**|包的唯一标识符 (ID)。|  
|name|**nvarchar(256)**|包的唯一名称。|  
|package_guid|**uniqueidentifier**|标识包的全局唯一标识符 (GUID)。|  
|description|**nvarchar(1024)**|包的可选描述。|  
|package_format_version|**int**|用于开发包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|version_major|**int**|包的主版本。|  
|version_minor|**int**|包的次版本。|  
|version_build|**int**|包的内部版本号。|  
|version_comments|**nvarchar(1024)**|包版本的可选注释。|  
|version_guid|**uniqueidentifier**|唯一标识包版本的 GUID。|  
|project_id|**bigint**|项目的唯一 ID。|  
|entry_point|**bit**|值为 `1` 表示直接启动包。 值为 `0` 表示该包由另一个包通过“执行包”任务启动。 默认值是`1`。|  
|validation_status|**char （1)**|验证的状态。|  
|last_validation_time|**datetimeoffset(7)**|最后验证的时间。|  
  
## <a name="remarks"></a>注释  
 此视图对于目录中的每个包显示一行。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对相应项目的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色。  
  
> [!NOTE]  
>  如果您对项目具有 READ 权限，则也对与该项目关联的所有包和环境引用具有 READ 权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

