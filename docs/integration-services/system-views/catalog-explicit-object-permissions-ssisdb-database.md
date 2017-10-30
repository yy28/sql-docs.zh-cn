---
title: "catalog.explicit_object_permissions （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 49b09e0f-06e8-451f-b979-a0d91000bfe3
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ce92a61241cb70f5e1c6d1bab8db8264d6228bd2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexplicitobjectpermissions-ssisdb-database"></a>catalog.explicit_object_permissions（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  仅显示已显式分配给此用户的权限。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_type|**int**|安全对象类型。 安全对象类型包括文件夹 (`1`）、项目 (`2`)、环境 (`3`） 和操作 (`4`)。|  
|object_id|**bigint**|安全对象的唯一标识符 (ID) 或主键。|  
|principal_id|**int**|数据库主体的 ID。|  
|permission_type|**int**|权限的类型。|  
|is_deny|**bit**|指示是已拒绝还是授予了该权限。 如果值为 `1`，则已拒绝此权限。 如果值为 `0`，则未拒绝此权限。|  
|grantor_id|**int**|授予该权限的主体的 ID。|  
  
## <a name="remarks"></a>注释  
 此视图显示下表中所列的权限类型：  
  
|permission_type 值|权限名称|权限说明|适用对象类型|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|允许主体读取被视为对象一部分的信息（如属性）。 它不允许主体枚举或读取该对象中包含的其他对象的内容。|文件夹、项目、环境、操作|  
|`2`|MODIFY|允许主体修改被视为对象一部分的信息（如属性）。 它不允许主体修改该对象中包含的其他对象。|文件夹、项目、环境、操作|  
|`3`|在运行 CREATE 语句前执行|允许主体执行项目中的所有包。|项目|  
|`4`|MANAGE_PERMISSIONS|允许主体向对象分配权限。|文件夹、项目、环境、操作|  
|`100`|CREATE_OBJECTS|允许主体在文件夹中创建对象。|文件夹|  
|`101`|READ_OBJECTS|允许主体读取文件夹中的所有对象。|文件夹|  
|`102`|MODIFY_OBJECTS|允许主体修改文件夹中的所有对象。|文件夹|  
|`103`|EXECUTE_OBJECTS|允许主体执行文件夹中所有项目的所有包。|文件夹|  
|`104`|MANAGE_OBJECT_PERMISSIONS|允许主体管理文件夹中所有对象的权限。|文件夹|  
  
## <a name="permissions"></a>Permissions  
 此视图并不显示当前主体的完整权限视图。 用户还必须检查主体是否为已分配了权限的角色和组的成员。  
  
  

