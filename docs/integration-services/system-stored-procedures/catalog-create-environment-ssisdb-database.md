---
title: "catalog.create_environment （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 66367092-9f6e-40e6-90bd-81efb078ab70
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 588728b6f86090e5b8f492ba3a117e0ccd47132e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironment-ssisdb-database"></a>catalog.create_environment（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建环境。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_environment [@folder_name =] folder_name  
     , [@environment_name =] environment_name  
  [  , [@environment_description =] environment_description ]  
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] *folder_name*  
 要包含环境的文件夹名称。 *Folder_name*是**nvarchar （128)**。  
  
 [@environment_name =] *environment_name*  
 环境的名称。 *Environment_name*是**nvarchar （128)**。  
  
 [@environment_description=] *environment_description*  
 环境的可选说明。 *Environment_description*是**nvarchar(1024)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对文件夹的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   找不到文件夹名称  
  
-   指定的文件夹中已存在同名的环境  
  
## <a name="remarks"></a>注释  
 环境名称在文件夹中必须是唯一的。  
  
  
