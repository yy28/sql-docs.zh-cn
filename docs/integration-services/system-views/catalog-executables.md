---
title: "catalog.executables |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aa0d2d5df7c3c39b1ad33794ae11c1a34ffe72d4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutables"></a>catalog.executables
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此视图为指定执行中的每个可执行文件都显示一行。  
  
 可执行文件是添加到包的控制流中的任务或容器。  
  
|列名|**数据类型**|Description|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|可执行文件的唯一标识符。|  
|execution_id|**bigint**|执行实例的唯一标识符。|  
|executable_name|**nvarchar(4000)**|可执行文件的名称。|  
|executable_guid|**nvarchar(38)**|可执行文件的 GUID。|  
|package_name|**nvarchar(260)**|包的名称。|  
|package_path|**nvarchar(max)**|包的路径。|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
## <a name="remarks"></a>注释  
  
