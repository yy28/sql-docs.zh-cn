---
title: catalog.move_project（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c79df90c6093ed93668e504e574c712a2ba2146a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716022"
---
# <a name="catalogmoveproject---ssisdb-database"></a>catalog.move_project - SSISDB 数据库

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将项目从一个文件夹移到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的另一个文件夹。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>参数  
 [ @source_folder = ] *source_folder*  
 此项目在移动之前所在的源文件夹的名称。 *source_folder* 为 **nvarchar(128)** 。  
  
 [ @project_name = ] project_name   
 要移动的项目的名称。 *project_name* 为 **nvarchar(128)** 。  
  
 [ @destination_folder = ] *destination_folder*  
 此项目在移动之后所在的目标文件夹的名称。 *destination_folder* 为 **nvarchar(128)** 。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对您想移动的项目的 READ 和 MODIFY 权限，以及针对目标文件夹的 CREATE_OBJECTS 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能导致此存储过程引发错误的情况：  
  
-   项目不存在。  
  
-   源文件夹不存在  
  
-   目标文件夹不存在，或目标文件夹已包含具有同名的项目  
  
-   用户没有相应的权限  
  
## <a name="remarks"></a>Remarks  
 当将项目从源文件夹移到目标文件夹时，将删除源文件夹中的项目和对应的环境引用。 在目标文件夹中，将创建相同的项目和环境引用。 在移动之后，相对环境引用将解析为不同的文件夹。 移动后，绝对引用将解析为同一文件夹。  
  
> [!NOTE]  
>  项目可以具有相对或绝对的环境引用。 相对引用通过名称引用环境，这些引用要求环境与项目位于相同文件夹中。 绝对引用通过名称和文件夹引用环境，这些引用引用与项目不在同一文件夹中的环境。  
  
  
