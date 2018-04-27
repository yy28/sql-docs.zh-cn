---
title: catalog.delete_project（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d74baea839dd45c402e02fe22f540efb644d1b5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个文件夹删除现有项目。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 包含项目的文件夹的名称。 folder_name 为 nvarchar(128)。  
  
 [ @project_name = ] project_name  
 要删除的项目的名称。 project_name 为 nvarchar(128)。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 和 MODIFY 权限  
  
-   ssis_admin 数据库角色的成员资格  
  
-   sysadmin 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能导致 delete_project 存储过程引发错误的情况：  
  
-   项目不存在。  
  
-   文件夹不存在  
  
-   用户没有相应的权限  
  
## <a name="remarks"></a>Remarks  
 对应项目的所有对象和环境引用将与项目一起删除。 但是，直到下次运行操作清除作业之前，将保留项目版本和相关的操作记录。  
  
  
