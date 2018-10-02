---
title: catalog.rename_folder（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 336ab467-c32f-4d2e-a79c-174dc6fab75e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a51dd95b42e462c10335e00d9c3b67545d9d07fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595425"
---
# <a name="catalogrenamefolder-ssisdb-database"></a>catalog.rename_folder（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中重命名一个文件夹。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.rename_folder [ @old_name = ] old_name , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>参数  
 [ @old_name = ] old_name  
 文件夹的原始名称。 old_name 为 nvarchar(128)。  
  
 [ @new_name = ] new_name  
 文件夹的新名称。 new_name 为 nvarchar(128)。  
  
## <a name="return-code-value"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   原始文件夹名称无效  
  
-   新名称已用于现有文件夹  
  
  
