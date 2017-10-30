---
title: "catalog.validate_project （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83439015694f4235af4a67e994e916651ec63cc1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidateproject-ssisdb-database"></a>catalog.validate_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以异步方式验证 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @validate_type =] *validate_type*  
 指示要执行的验证类型。 使用字符 `F` 执行完全验证。 *Validate_type*是**char （1)**。  
  
 [ @validation_id =] *validation_id*  
 返回验证的唯一标识符 (ID)。 *Validation_id*是**bigint**。  
  
 [ @use32bitruntime =] *use32bitruntime*  
 指示是否应使用 32 位运行时在 64 位操作系统上运行包。 使用的值`1`时要执行与 32 位运行时包在 64 位操作系统上运行。 在 64 位操作系统上运行时，使用值 `0` 以便使用 64 位运行时执行此包。 此参数可选。 *Use32bitruntime*是**位**。  
  
 [ @environment_scope =] *environment_scope*  
 指示由验证考虑的环境引用。 如果值为 `A`，则验证中包括与项目关联的所有环境引用。 值为 `S` 时，只包括一个环境引用。 当值为 `D` 时，不包括环境引用，并且每个参数必须有文字默认值才能通过验证。 此参数是可选的字符`D`默认情况下将使用。 *Environment_scope*是**char （1)**。  
  
 [ @reference_id =] *reference_id*  
 环境引用的唯一 ID。 此参数是必需的仅当单个环境引用包含在验证中，当*environment_scope*是`S`。 *Reference_id*是**bigint**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 验证步骤的输出结果作为结果集的不同部分返回。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   项目的读取的权限，如果适用，在引用环境上的读取权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表提供了一些可能引发错误或警告的情况：  
  
-   验证针对项目中的一个或多个包失败  
  
-   如果验证中包含的一个或多个引用环境不包含引用的变量，则验证失败  
  
-   指定的验证类型无效  
  
-   项目名称或环境引用 ID 无效  
  
-   用户没有适当的权限  
  
## <a name="remarks"></a>注释  
 验证有助于识别将阻止项目中的包成功运行的问题。 使用[catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md)或[catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)视图来验证状态的监视器。  
  
 在验证中只可使用此用户可访问的环境。 验证输出作为结果集发送到客户端。  
  
 在这一版本中，项目验证不支持依赖项验证。  
  
 完全验证确认在验证包含的引用环境中可以找到所有引用的环境变量。 完全验证结果列出了无效的环境引用和在验证中包含的任何引用环境中找不到的引用环境变量。  
  
  

