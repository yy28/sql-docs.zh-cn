---
title: catalog.extended_operation_info（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 360c51b7f1accd1c21b2026d8ae33dba463db72d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747155"
---
# <a name="catalogextendedoperationinfo-ssisdb-database"></a>catalog.extended_operation_info（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有操作的扩展信息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|扩展信息的唯一标识符 (ID)。|  
|operation_id|**bigint**|对应于扩展信息的操作的唯一 ID。|  
|object_name|nvarchar(260)|对象的名称。|  
|object_type|**smallint**|受操作影响的对象的类型。 该对象可能是文件夹 (`10`）、项目 (`20`）、包 (`30`)、环境 (`40`） 或执行实例 （`50`)。|  
|reference_id|**bigint**|操作中使用的引用的唯一 ID。|  
|status|**int**|操作的状态。 可能的值是已创建 (`1`)、正在运行 (`2`)、已取消 (`3`)、失败 (`4`)、挂起 (`5`)、意外结束 (`6`)、已成功 (`7`)、停止 (`8`) 和已完成 (`9`)。|  
|start_time|**datetimeoffset(7)**|操作开始的日期和时间。|  
|end_time|**datetimeoffset(7)**|操作结束的日期和时间。|  
  
## <a name="remarks"></a>Remarks  
 单个操作可以有多个扩展的信息行。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对操作的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
