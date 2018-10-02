---
title: catalog.set_folder_description（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 159eae51815fcb5343e81dd500dc55de90250e99
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668015"
---
# <a name="catalogsetfolderdescription-ssisdb-database"></a>catalog.set_folder_description（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置文件夹的说明。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name = ] folder_name  
 文件夹的名称。 *folder_name* 为 **nvarchar(128)**。  
  
 [ @folder_description = ] folder_description  
 文件夹的说明。 folder_description 为 nvarchar(MAX)。  
  
## <a name="return-code-value"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 存储过程返回一条消息，以确认新文件夹说明的设置。  
  
  
