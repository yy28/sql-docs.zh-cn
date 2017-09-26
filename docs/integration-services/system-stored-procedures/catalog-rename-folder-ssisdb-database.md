---
title: "catalog.rename_folder （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 336ab467-c32f-4d2e-a79c-174dc6fab75e
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8320f1a4d4fb08e206e2dcde2e5158b5dd0729aa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenamefolder-ssisdb-database"></a>catalog.rename_folder（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中重命名一个文件夹。  
  
## <a name="syntax"></a>语法  
  
```tsql  
rename_folder [ @old_name = ] old_name , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>参数  
 [ @old_name =] *old_name*  
 文件夹的原始名称。 *Old_name*是**nvarchar （128)**。  
  
 [ @new_name =] *new_name*  
 文件夹的新名称。 *New_name*是**nvarchar （128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   原始文件夹名称无效  
  
-   新名称已用于现有文件夹  
  
  
