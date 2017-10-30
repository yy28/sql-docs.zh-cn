---
title: "catalog.folders （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9622bd1a5f1415c9f506a00a63441081154b53ff
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的文件夹。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|id|**bigint**|文件夹的唯一标识符。|  
|name|**sysname(nvarchar(128)**|文件夹的名称，此名称在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中是唯一的。|  
|description|**nvarchar(1024)**|文件夹的说明。|  
|created_by_sid|**varbinary(85)**|创建了文件夹的用户的安全标识符 (SID)。|  
|created_by_name|**nvarchar （128)**|创建文件夹的用户名。|  
|created_time|**datetimeoffset(7)**|创建文件夹的日期和时间。|  
  
## <a name="remarks"></a>注释  
 此视图对于目录中的每个文件夹显示一行。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对文件夹的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

