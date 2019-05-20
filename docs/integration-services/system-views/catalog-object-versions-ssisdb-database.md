---
title: catalog.object_versions（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b68fcc0cffada1ac895548a0c6858f0bde76fe6c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714487"
---
# <a name="catalogobjectversions-ssisdb-database"></a>catalog.object_versions（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中对象的版本。 在此版本中，此视图只支持项目的版本。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|对象版本的唯一标识符 (ID)。 此数字不保证是按顺序排列的。|  
|object_id|**bigint**|对象的唯一 ID。|  
|object_type|**smallint**|对象的类型。 将针对项目显示值 `20`。|  
|object_name|**sysname(nvarchar(128))**|对象的名称。|  
|description|**nvarchar(1024)**|项目的说明。|  
|created_by|**nvarchar(128)**|向目录添加对象的用户名。|  
|created_time|**datetimeoffset**|将对象添加到目录中的日期和时间。|  
|restored_by|**nvarchar(128)**|还原对象的用户名。|  
|last_restored_time|**datetimeoffset**|上次还原对象的日期和时间。|  
  
## <a name="remarks"></a>Remarks  
 此视图对于目录中的每个对象版本显示一行。  
  
## <a name="permissions"></a>权限  
 若要查看此视图中的行，您必须具有以下权限之一：  
  
-   针对对象的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   sysadmin 服务器角色中的成员资格。  
  
> [!NOTE]  
>  将实施行级安全性；只显示您有权查看的行。  
  
  
