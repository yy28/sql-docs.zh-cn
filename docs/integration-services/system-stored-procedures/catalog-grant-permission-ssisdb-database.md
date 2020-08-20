---
description: catalog.grant_permission（SSISDB 数据库）
title: catalog.grant_permission（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19ad48a806db4f1877ac71f38d71be8f0d2dadc6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495394"
---
# <a name="cataloggrant_permission-ssisdb-database"></a>catalog.grant_permission（SSISDB 数据库）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  授予对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个安全对象的权限。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>参数  
 [ @object_type = ] *object_type*  
 安全对象的类型。 安全对象类型包括文件夹 (`1`）、项目 (`2`)、环境 (`3`) 和操作 (`4`)。*object_type* 为 **smallint** _。_  
  
 [ @object_id = ] *object_id*  
 安全对象的唯一标识符 (ID)。 *object_id* 为 **bigint**。  
  
 [ @principal_id = ] *principal_id*  
 要被授予权限的主体的 ID。 *principal_id* 为 **int**。  
  
 [ @permission_type = ] *permission_type*  
 要授予的权限的类型。 *permission_type* 为 **smallint**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）  
  
 1（object_class 无效）  
  
 2（object_id 不存在）  
  
 3（主体不存在）  
  
 4（权限无效）  
  
 5（其他错误）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对对象的 ASSIGN_PERMISSIONS 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  

此过程不能由 SQL Server 验证了身份的登录名调用。 它不能由 sa 登录名调用。
  
## <a name="remarks"></a>注解  
 通过此存储过程可以授予下表中所示的权限类型：  
  
|permission_type 值|权限名称|权限说明|适用对象类型|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|允许主体读取被视为对象一部分的信息（如属性）。 它不允许主体枚举或读取该对象中包含的其他对象的内容。|文件夹、项目、环境、操作|  
|`2`|MODIFY|允许主体修改被视为对象一部分的信息（如属性）。 它不允许主体修改该对象中包含的其他对象。|文件夹、项目、环境、操作|  
|`3`|EXECUTE|允许主体执行项目中的所有包。|项目|  
|`4`|MANAGE_PERMISSIONS|允许主体向对象分配权限。|文件夹、项目、环境、操作|  
|`100`|CREATE_OBJECTS|允许主体在文件夹中创建对象。|文件夹|  
|`101`|READ_OBJECTS|允许主体读取文件夹中的所有对象。|文件夹|  
|`102`|MODIFY_OBJECTS|允许主体修改文件夹中的所有对象。|文件夹|  
|`103`|EXECUTE_OBJECTS|允许主体执行文件夹中所有项目的所有包。|文件夹|  
|`104`|MANAGE_OBJECT_PERMISSIONS|允许主体管理文件夹中所有对象的权限。|文件夹|  
  
## <a name="errors-and-warnings"></a>错误和警告  
 有关相关错误和消息，请参阅“返回代码值”一节。  
  
  
