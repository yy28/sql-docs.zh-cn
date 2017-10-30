---
title: "catalog.clear_object_parameter_value （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  清除存储在服务器上的现有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目或包的参数的值。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @object_type =] *object_type*  
 对象的类型。 有效值包括 `20`（对应于项目）和 `30`（对应于包）。 *Object_type*是**smallInt**。  
  
 [@ 对象 _name =]*对象 _name*  
 包的名称。 *对象 _name*是**nvarchar(260)**。  
  
 [@parameter_名称 =] *parameter_name*  
 参数名。 *Parameter_ 名称*是**nvarchar （128)**。  
  
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
 下面介绍了一些条件会导致引发错误的 clear_object_parameter 存储过程：  
  
-   指定了无效的对象类型，或在项目中找不到对象名称。  
  
-   项目不存在、项目无法访问，或者项目名称无效  
  
-   指定了无效的参数名称。  
  
-   用户不具备适当的权限。  
  
  

