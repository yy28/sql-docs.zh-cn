---
title: "catalog.set_object_parameter_value （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9c27cff7ad828ab5c19183febd2ad562d5c9b925
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置参数的值。 将值与环境变量关联，或者如果未指定任何其他值，则分配默认情况下使用的文本值。  
  
## <a name="syntax"></a>语法  
  
```tsql  
set_object_parameter_value [ @object_type = ] object_type   
    , [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @parameter_name = ] parameter _name   
    , [ @parameter_value = ] parameter_value   
 [  , [ @object_name = ] object_name ]  
 [  , [ @value_type = ] value_type ]  
```  
  
## <a name="arguments"></a>参数  
 [ @object_type =] *object_type*  
 参数的类型。 使用值 `20` 表示项目参数，使用值 `30` 表示包参数。 *Object_type*是**smallInt**。  
  
 [ @folder_name =] *folder_name*  
 包含参数的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 包含参数的项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @parameter_name =] *parameter_name*  
 参数名。 *Parameter_name*是**nvarchar （128)**。  
  
 [ @parameter_value =] *parameter_value*  
 参数的值。 *Parameter_value*是**sql_variant**。  
  
 [ @object_name =] *object_name*  
 包的名称。 当参数为包参数时，需要此参数。 *Object_name*是**nvarchar(260)**。  
  
 [ @value_type =] *value_type*  
 参数值的类型。 使用字符`V`，则指示*parameter_value*是在执行之前分配一个文本值，将使用默认情况下的其他任何值。 使用字符`R`，则指示*parameter_value*是一个引用的值，已设置为环境变量的名称。 此参数是可选的，默认情况下，将使用 `V` 字符。 *Value_type*是**char （1)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能导致此存储过程引发错误的情况：  
  
-   参数类型无效。  
  
-   项目名称无效  
  
-   对于包参数，项目名称无效  
  
-   值类型无效  
  
-   用户没有适当的权限  
  
## <a name="remarks"></a>注释  
  
-   如果没有*value_type*指定，则为一个文本值*parameter_value*默认情况下使用。 当使用某一文字值时， *value_set*中[object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)视图设为`1`。 不允许 NULL 参数值。  
  
-   如果*value_type*包含字符`R`，这表示一个引用的值， *parameter_value*引用环境变量的名称。  
  
-   值`20`可以用来进行*object_type*来表示项目参数。 为此示例中，输入值*object_name*有必要，并指定任何值不是*object_name*将被忽略。 当用户要设置项目参数时，将使用此值。  
  
-   值`30`可以用来进行*object_type*来表示包参数。 为此示例中，输入值*object_name*用于表示相应的包。 如果*object_name*未指定，存储的过程返回一个错误并终止。  
  
  
