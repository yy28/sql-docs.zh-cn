---
title: "catalog.deploy_project （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5682cd23cb65e097bccb8cc69d5f2ec88ece7709
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的文件夹，或更新以前部署的现有项目。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] *folder_name*  
 部署项目中的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [@project_name =]*文件的内容*  
 文件夹中新的或更新的项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [@projectstream =] *projectstream*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署文件（扩展名为.ispac）的二进制内容。  
  
 您可以使用带 OPENROWSET 函数的 SELECT 语句以及大容量行集提供程序来检索该文件的二进制内容。 有关示例，请参阅[部署 Integration Services (SSIS) 项目和包](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。 有关 OPENROWSET 的详细信息，请参阅[OPENROWSET &#40;Transact SQL &#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
 *Projectstream*是**varbinary （max)**  
  
 [@operation_id =] *operation_id*  
 返回部署操作的唯一标识符。 *Operation_id*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   对文件夹具有 CREATE_OBJECTS 权限才能部署新项目；对项目具有 MODIFY 权限才能更新项目  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 以下列表描述某些可能会导致此存储的过程以引发错误的情况：  
  
-   参数引用的对象不存在，参数试图创建的对象已存在，或者参数在某个其他方面无效  
  
-   参数的值 *@project_name* 的部署文件中的项目的名称不匹配  
  
-   用户不具备足够的权限  
  
## <a name="remarks"></a>注释  
 在项目部署或更新期间，存储过程不检查项目中各个包的保护级别。  
  
  

