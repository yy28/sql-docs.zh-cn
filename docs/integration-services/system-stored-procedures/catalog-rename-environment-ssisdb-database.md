---
title: "catalog.rename_environment （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d3ca0f18c9ea11105ebb575d2f5db449f91e4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenameenvironment-ssisdb-database"></a>catalog.rename_environment（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中重命名环境。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含环境的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @environment_name =] *environment_name*  
 环境的原始名称。 *Environment_name*是**nvarchar （128)**。  
  
 [ @new_environment_name =] *new_environment_name*  
 环境的新名称。 *New_environment_name*是**nvarchar （128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对环境的 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   原始环境名称无效  
  
-   新名称已用于现有环境  
  
## <a name="remarks"></a>注释  
 当您重命名环境时，项目中的环境引用不会自动更新。 必须相应地更新环境引用。 即使通过更改环境名称损坏了环境引用，此存储过程也会成功。 在此存储过程完成之后，必须更新环境引用。  
  
> [!NOTE]  
>  当一个环境引用无效时，对使用这些引用的包进行验证和执行将失败。  
  
  
