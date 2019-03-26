---
title: catalog.create_environment_reference（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7230c0fe7263d16f3b61aefac6f7a55a465b2f8c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290663"
---
# <a name="catalogcreateenvironmentreference-ssisdb-database"></a>catalog.create_environment_reference（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中为项目创建环境引用。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_location = ] reference_location  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 正在引用环境的项目的文件夹名称。 *folder_name* 为 **nvarchar(128)**。  
  
 [ @project_name = ] project_name  
 正在引用环境的项目的名称。 *project_name* 为 **nvarchar(128)**。  
  
 [ @environment_name = ] environment_name  
 被引用环境的名称。 environment_name 为 nvarchar(128)。  
  
 [ @reference_location = ] reference_location  
 指示环境是可以位于与项目相同的文件夹中（相对引用），还是位于其他文件夹中（绝对引用）中。 使用值 `R` 指示相对引用。 使用值 `A` 指示绝对引用。 reference_location 为 char(1)。  
  
 [ @environment_folder_name = ] environment_folder_name  
 被引用的环境所在的文件夹的名称。 此值对于绝对引用是必需的。 environment_folder_name 为 nvarchar(128)。  
  
 [ @reference_id = ] reference_id  
 返回新引用的唯一标识符。 此参数可选。 reference_id 为 bigint。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 和 MODIFY 权限，以及针对环境的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   文件夹名称无效  
  
-   项目名称无效  
  
-   用户没有相应的权限  
  
-   通过使用 reference_location 参数中的 `A` 字符指定绝对引用，而未使用 environment_folder_name 参数指定该文件夹的名称。  
  
## <a name="remarks"></a>Remarks  
 项目可以具有相对或绝对的环境引用。 相对引用通过名称引用环境，并要求它与项目位于相同文件夹中。 绝对引用通过名称和文件夹引用环境，可能引用与项目不在同一文件夹中的环境。 项目可以引用多个环境。  
  
  
