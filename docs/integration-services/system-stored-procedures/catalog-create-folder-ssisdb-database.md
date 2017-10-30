---
title: "catalog.create_folder （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 43d128f9dcc4cea632c810a13d21eb5e1ddb61df
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建一个文件夹。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] *folder_name*  
 新文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [@folder_name =] *folder_id*  
 文件夹的唯一标识符 (ID)。 *Folder_id*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 返回文件夹标识符。  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
如果已存在具有相同名称的文件夹，存储的过程将返回错误。  
  
  

