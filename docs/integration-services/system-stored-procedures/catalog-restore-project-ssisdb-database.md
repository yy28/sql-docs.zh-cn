---
title: "catalog.restore_project （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目还原到以前的版本。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project _name =]*文件的内容*  
 项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @object_version_lsn =] *object_version_lsn*  
 项目的版本。 *Object_version_lsn*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 项目详细信息将作为返回**varbinary （max)**的结果集如果一部分*文件的内容*找到。  
  
 **没有结果集**返回如果无法将项目还原到指定的文件夹。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   项目版本不存在，或与项目名称不匹配  
  
-   项目不存在。  
  
-   用户没有适当的权限  
  
## <a name="remarks"></a>注释  
 还原某个项目后，将为所有参数分配默认值，并且所有环境引用都保持不变。 项目版本的目录中保留最大数量由目录属性**MAX_VERSIONS_PER_PROJECT**中, 所示[catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)视图。  
  
> [!WARNING]  
>  在还原项目后，环境引用可能不再有效。  
  
  
