---
title: "catalog.set_environment_reference_type （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e83d9979ee4736528efb4851848ea3eac717fab8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  设置与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中某个项目的现有环境引用关联的引用类型和环境名称。  
  
## <a name="syntax"></a>语法  
  
```sql  
set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>参数  
 [ @reference_id =] *reference_id*  
 要更新的环境引用的唯一标识符。 *Reference_id*是**bigint**。  
  
 [ @reference_type =] *reference_type*  
 指示环境是可以位于与项目相同的文件夹中（相对引用），还是位于其他文件夹中（绝对引用）中。 使用值 `R` 指示相对引用。 使用值 `A` 指示绝对引用。 *Reference_type*是**char （1)**。  
  
 [ @environment_folder_name =] *environment_folder_name*  
 环境所在的文件夹。 此值对于绝对引用是必需的。 *Environment_folder_name*是**nvarchar （128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 和 MODIFY 权限，以及针对环境的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   文件夹名称、环境名称或引用 ID 无效  
  
-   用户不适宜权限  
  
-   使用指定的绝对引用`A`字符中*reference_location*参数，但文件夹的名称未指定与*environment_folder_name*参数。  
  
## <a name="remarks"></a>注释  
 项目可以具有相对或绝对的环境引用。 相对引用通过名称引用环境，并要求它与项目位于相同文件夹中。 绝对引用通过名称和文件夹引用环境，可能引用与项目不在同一文件夹中的环境。 项目可以引用多个环境。  
  
> [!IMPORTANT]  
>  如果指定了相对的引用， *environment_folder_name*不使用参数值，并且环境文件夹名称将自动设置为**NULL**。 如果指定的绝对引用，则必须在提供环境文件夹名称*environment_folder_name*参数。  
  
  
