---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0a1828925494ca2e1e8f593e3f133a21cd10a9ee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296777"
---
# <a name="catalogdeploy_packages"></a>catalog.deploy_packages 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将一个或多个包部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的文件夹，或更新以前部署的现有包。  
  
## <a name="syntax"></a>语法  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name   
 文件夹的名称。 *folder_name* 为 **nvarchar(128)** 。  
  
 [ @project_name = ] project_name   
 文件夹中项目的名称。 *project_name* 为 **nvarchar(128)** 。  
  
 [ @packages_table = ] *packages_table*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包 (.dtsx) 文件的二进制内容。 *packages_table* 为 **[catalog].[Package_Table_Type]**  
  
 [ @operation_id = ] operation_id   
 返回部署操作的唯一标识符。 operation_id 为 bigint   。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   对项目具有 CREATE_OBJECTS 权限或对包具有 MODIFY 权限才能更新包。  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能导致此存储过程引发错误的情况：  
  
-   参数引用的对象不存在，参数试图创建的对象已存在，或者参数在其他某个方面无效。  
  
-   用户不具备足够的权限  
  
  
