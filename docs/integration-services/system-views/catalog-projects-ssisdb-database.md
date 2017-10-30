---
title: "catalog.projects （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 668890ae464deb8dfa029eab38b608fee12af0ca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示中显示的所有项目的详细信息**SSISDB**目录。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|项目的唯一标识符 (ID)。|  
|folder_id|**bigint**|项目位于其中的文件夹的唯一 ID。|  
|name|**sysname**|项目的名称。|  
|description|**nvarchar(1024)**|项目的可选说明。|  
|project_format_version|**int**|用于开发项目的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|deployed_by_sid|**varbinary(85)**|安装了项目的用户的安全标识符 (SID)。|  
|deployed_by_name|**nvarchar （128)**|安装项目的用户名。|  
|last_deployed_time|**datetimeoffset(7)**|部署或重新部署项目的日期和时间。|  
|created_time|**datetimeoffset(7)**|日期和时间在其中创建项目。|  
|object_version_lsn|**bigint**|项目的版本。 此数字不保证是按顺序排列的。|  
|validation_status|**char （1)**|验证状态。|  
|last_validation_time|**datetimeoffset(7)**|最后验证的时间。|  
  
## <a name="remarks"></a>注释  
 此视图对于目录中的每个项目显示一行。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对项目的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色。  
  
> [!NOTE]  
>  如果您对项目具有 READ 权限，则也对与该项目关联的所有包和环境引用具有 READ 权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

