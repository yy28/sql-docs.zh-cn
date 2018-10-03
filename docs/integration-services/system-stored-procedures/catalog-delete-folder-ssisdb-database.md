---
title: catalog.delete_folder（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b9c08992-500c-447e-bc19-1eb13c9b0293
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae60521ebd4b3bf9d10e12d5f15a54ceb0166c04
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626135"
---
# <a name="catalogdeletefolder-ssisdb-database"></a>catalog.delete_folder（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录删除文件夹。  
  
## <a name="syntax"></a>语法  
  
```sql  
delete_folder [ @folder_name = ] folder_name  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 要删除的文件夹的名称。 *folder_name* 为 **nvarchar(128)**。  
  
## <a name="return-code-value"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 将返回一条消息以确认删除文件夹。  
  
  
