---
title: catalog.projects（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 106b9a3e90a9a7ce872ea215e15287283adfadd2
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408839"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 **SSISDB** 目录中显示的所有项目的详细信息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|项目的唯一标识符 (ID)。|  
|folder_id|**bigint**|项目位于其中的文件夹的唯一 ID。|  
|NAME|**sysname**|项目的名称。|  
|description|**nvarchar(1024)**|项目的可选说明。|  
|project_format_version|**int**|用于开发项目的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|deployed_by_sid|**varbinary(85)**|安装了项目的用户的安全标识符 (SID)。|  
|deployed_by_name|**nvarchar(128)**|安装项目的用户名。|  
|last_deployed_time|**datetimeoffset(7)**|部署或重新部署项目的日期和时间。|  
|created_time|**datetimeoffset(7)**|项目的创建日期和时间。|  
|object_version_lsn|**bigint**|项目的版本。 此数字不保证是按顺序排列的。|  
|validation_status|**char(1)**|验证状态。|  
|last_validation_time|**datetimeoffset(7)**|最后验证的时间。|  
  
## <a name="remarks"></a>Remarks  
 此视图对于目录中的每个项目显示一行。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对项目的 READ 权限  
  
-   ssis_admin 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格。  
  
> [!NOTE]  
>  如果您对项目具有 READ 权限，则也对与该项目关联的所有包和环境引用具有 READ 权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
