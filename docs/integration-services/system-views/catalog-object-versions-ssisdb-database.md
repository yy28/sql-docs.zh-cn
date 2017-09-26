---
title: "catalog.object_versions （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3ea7c5ae054a002b9bb4f150e60f323ae03d702a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectversions-ssisdb-database"></a>catalog.object_versions（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中对象的版本。 在此版本中，此视图只支持项目的版本。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|对象版本的唯一标识符 (ID)。 此数字不保证是按顺序排列的。|  
|object_id|**bigint**|对象的唯一 ID。|  
|object_type|**int**|对象的类型。 将针对项目显示值 `20`。|  
|object_name|**sysname(nvarchar(128))**|对象的名称。|  
|description|**nvarchar(1024)**|项目的说明。|  
|created_by|**nvarchar （128)**|向目录添加对象的用户名。|  
|created_time|**datetimeoffset**|将对象添加到目录中的日期和时间。|  
|restored_by|**nvarchar （128)**|还原对象的用户名。|  
|last_restored_time|**datetimeoffset**|上次还原对象的日期和时间。|  
  
## <a name="remarks"></a>注释  
 此视图对于目录中的每个对象版本显示一行。  
  
## <a name="permissions"></a>Permissions  
 若要查看此视图中的行，您必须具有以下权限之一：  
  
-   针对对象的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   中的成员身份**sysadmin**服务器角色。  
  
> [!NOTE]  
>  将实施行级安全性；只显示您有权查看的行。  
  
  
