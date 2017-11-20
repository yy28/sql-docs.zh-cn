---
title: "catalog.execution_property_override_values |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ed9ae4ea7a7165efe53a551832d8e4a0eb7a2114
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在包执行期间设置的属性覆盖值。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|属性覆盖值的唯一 ID。|  
|execution_id|**bigint**|执行实例的唯一 ID。|  
|property_path|**nvarchar(4000)**|指向包中属性的路径。|  
|property_value|**nvarchar(max)**|属性的覆盖值。|  
|sensitive|**bit**|当值为 1 时，属性是敏感的并在存储时加密。 当值为 0 时，属性是不敏感的并以纯文本形式存储值。|  
  
## <a name="remarks"></a>注释  
 此视图显示中属性值已使用重写每次执行一行**属性重写**主题中**高级**选项卡**执行包**对话框。 属性的路径派生自**包路径**包任务的属性。  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

