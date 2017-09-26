---
title: "catalog.delete_environment_variable （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 894b3bdb-aa34-463e-aba4-1b68ad96a0ef
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bd3ff266d41d4e62d5ecb9314a14de7e1b86d8d5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeleteenvironmentvariable-ssisdb-database"></a>catalog.delete_environment_variable（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个环境删除环境变量。  
  
## <a name="syntax"></a>语法  
  
```tsql  
delete_environment_variable [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含环境的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @environment_name =] *environment_name*  
 包含变量的环境的名称。 *Environment_name*是**nvarchar （128)**。  
  
 [ @variable_name =] *variable_name*  
 包含要删除的变量的名称。 *Variable_name*是**nvarchar （128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对环境的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   环境名称无效  
  
-   环境变量不存在  
  
  
