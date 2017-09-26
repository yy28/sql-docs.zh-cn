---
title: "catalog.delete_project （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: abc0280a693be8e0f9fa9b3ec997c1d38d96ed54
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个文件夹删除现有项目。  
  
## <a name="syntax"></a>语法  
  
```tsql  
delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 要删除的项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
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
 下面介绍了一些条件会导致引发错误的 delete_project 存储过程：  
  
-   项目不存在。  
  
-   文件夹不存在  
  
-   用户没有适当的权限  
  
## <a name="remarks"></a>注释  
 对应项目的所有对象和环境引用将与项目一起删除。 但是，直到下次运行操作清除作业之前，将保留项目版本和相关的操作记录。  
  
  
