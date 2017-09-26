---
title: "catalog.set_folder_description （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f707687b62be599d74bde892f86ff50754185ff8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetfolderdescription-ssisdb-database"></a>catalog.set_folder_description（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置文件夹的说明。  
  
## <a name="syntax"></a>语法  
  
```tsql  
set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @folder_description =] *folder_description*  
 文件夹的说明。 *Folder_description*是**nvarchar (max)**。  
  
## <a name="return-code-value"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 存储过程返回一条消息，以确认新文件夹说明的设置。  
  
  
