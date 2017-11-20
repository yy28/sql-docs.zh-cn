---
title: "catalog.deny_permission （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: de310bac-2ddc-4ef9-8783-43dcb02a94f1
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 689a59e92286881fa3be7ee3754a786ccb54ae6c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdenypermission-ssisdb-database"></a>catalog.deny_permission（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  拒绝对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个安全对象的权限。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.deny_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>参数  
 [ @object_type =] *object_type*  
 安全对象类型。 安全对象类型包括文件夹 (`1`)，项目 (`2`)，环境 (`3`)，和操作 (`4`)。*Object_type*是**smallint***。*  
  
 [ @object_id =] *object_id*  
 唯一标识符 (ID) 或安全对象的主键。 *Object_id*是**bigint**。  
  
 [ @principal_id =] *principal_id*  
 被拒绝的主体的 ID。 *Principal_id*是**int**。  
  
 [ @permission_type =] *permission_type*  
 要被拒绝的权限类型。 *Permission_type*是**smallint**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）  
  
 1 （object_class 不是有效的）  
  
 2 （object_id 不存在）  
  
 3 （主体不存在）  
  
 4 （权限不是有效的）  
  
 5（其他错误）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对对象的 MANAGE_PERMISSIONS 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="remarks"></a>注释  
 通过此存储过程可以拒绝下表中所示的权限类型：  
  
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
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   如果指定 permission_type，则该过程将拒绝指定显式分配给指定的对象的指定主体的权限。 即使不发生此类情况，该过程也仍将返回成功代码值 (`0`)。  
  
-   如果省略 permission_type，过程将拒绝对指定的对象指定的主体的所有权限。  
  
  

