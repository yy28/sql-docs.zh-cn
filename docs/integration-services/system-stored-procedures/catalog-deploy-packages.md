---
title: "catalog.deploy_packages |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将一个或多个包部署到一个文件夹中[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]目录或更新以前已部署的现有包。  
  
## <a name="syntax"></a>语法  
  
```  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 项目的文件夹中的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @packages_table =] *packages_table*  
 二进制内容组成[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包 (.dtsx) 文件。 *Packages_table*是**[目录]。 [Package_Table_Type]**  
  
 [ @operation_id =] *operation_id*  
 返回部署操作的唯一标识符。 *Operation_id*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   CREATE_OBJECTS 项目或包的修改权限，要更新的包上的权限。  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 以下列表描述某些可能会导致此存储的过程以引发错误的情况：  
  
-   参数引用不存在的对象、 参数尝试创建一个对象，已存在，或以某种其他方式的参数无效。  
  
-   用户不具备足够的权限  
  
  
