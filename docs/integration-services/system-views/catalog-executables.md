---
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 495a60de43826e633ee6c8eb2bcc7d38cf07706b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912613"
---
# <a name="catalogexecutables"></a>catalog.executables 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  此视图为指定执行中的每个可执行文件都显示一行。  
  
 可执行文件是添加到包的控制流中的任务或容器。  
  
|列名称|**Data type**|说明|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|可执行文件的唯一标识符。|  
|execution_id|**bigint**|执行实例的唯一标识符。|  
|executable_name|**nvarchar(4000)**|可执行文件的名称。|  
|executable_guid|**nvarchar(38)**|可执行文件的 GUID。|  
|package_name|nvarchar(260) |包的名称。|  
|package_path|**nvarchar(max)**|包的路径。|  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
## <a name="remarks"></a>备注  
  
