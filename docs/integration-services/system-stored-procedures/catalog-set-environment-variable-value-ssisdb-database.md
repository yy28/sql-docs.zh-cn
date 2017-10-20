---
title: "catalog.set_environment_variable_value （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f30937f6dca19f82ccb2dc8ac998dd9f9510c0f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentvariablevalue-ssisdb-database"></a>catalog.set_environment_variable_value（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境变量的值。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含环境的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @environment_name =] *environment_name*  
 环境的名称。 *Environment_name*是**nvarchar （128)**。  
  
 [ @variable _name =]*变量 _name*  
 环境变量的名称。 *变量 _name*是**nvarchar （128)**。  
  
 [ @value =]*值*  
 环境变量的值。 *值*是**sql_variant**。  
  
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
  
-   文件夹名称无效  
  
-   环境名称无效  
  
-   环境变量名称无效  
  
-   用户不具备适当的权限  
  
  
