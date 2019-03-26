---
title: catalog.get_project（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28fe8cd113404d2a5672daa249c80f3b3d91620c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275022"
---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  检索已部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的项目的二进制流。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 包含项目的文件夹的名称。 folder_name 为 nvarchar(128)。  
  
 [ @project_name = ] project_name  
 项目的名称。 project_name 为 nvarchar(128)。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 该项目的二进制流作为 varbinary(MAX) 返回。 如果找不到文件夹或项目，则不返回任何结果。  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 权限  
  
-   ssis_admin 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能导致 get_project 存储过程引发错误的情况：  
  
-   项目不存在。  
  
-   文件夹不存在  
  
-   用户没有相应的权限  
  
  
