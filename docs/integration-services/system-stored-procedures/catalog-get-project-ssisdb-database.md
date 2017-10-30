---
title: "catalog.get_project （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: adb3542d50db426d5908aa8786145406d7263ad6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  检索已部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的项目的二进制流。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 作为返回项目的二进制流**varbinary （max)**。 如果找不到文件夹或项目，则不返回任何结果。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   读取权限项目  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面介绍了一些条件会导致引发错误的 get_project 存储过程：  
  
-   项目不存在。  
  
-   文件夹不存在  
  
-   用户没有适当的权限  
  
  
