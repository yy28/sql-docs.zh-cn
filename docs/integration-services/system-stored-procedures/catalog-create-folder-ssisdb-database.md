---
title: catalog.create_folder（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8053d269d13b0eeaf244d0170c090470a6c47a49
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406849"
---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建一个文件夹。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] folder_name  
 新文件夹的名称。 folder_name 为 nvarchar(128)。  
  
 [@folder_name =] folder_id  
 文件夹的唯一标识符 (ID)。 folder_id 为 bigint。  
  
## <a name="return-code-value"></a>返回代码值  
 返回文件夹标识符。  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   ssis_admin 数据库角色的成员资格  
  
-   sysadmin 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
如果已存在同名的文件夹，改存储过程返回错误。  
  
  
