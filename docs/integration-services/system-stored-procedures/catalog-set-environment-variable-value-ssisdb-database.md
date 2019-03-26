---
title: catalog.set_environment_variable_value（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 352577a69ba10f7eb6e2ef6e5b4e5900bf0629f6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274112"
---
# <a name="catalogsetenvironmentvariablevalue-ssisdb-database"></a>catalog.set_environment_variable_value（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境变量的值。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 包含环境的文件夹的名称。 *folder_name* 为 **nvarchar(128)**。  
  
 [ @environment_name = ] environment_name  
 环境的名称。 environment_name 为 nvarchar(128)。  
  
 [ @variable _name = ] variable _name  
 环境变量的名称。 variable _name 为 nvarchar(128)。  
  
 [ @value = ] value  
 环境变量的值。 value 为 sql_variant。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对环境的 READ 和 MODIFY 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   文件夹名称无效  
  
-   环境名称无效  
  
-   环境变量名称无效  
  
-   用户不具备适当的权限  
  
  
