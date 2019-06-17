---
title: sysdac_instances_internal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1e30db7b31a0a29a5e78e7fc5876f43764d66a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471109"
---
# <a name="data-tier-application-tables---sysdacinstancesinternal"></a>数据层应用程序表 - sysdac_instances_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个数据层应用程序 (DAC) 实例显示一行。 此表存储在 msdb 数据库中的 dbo 架构。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC 实例的标识符。|  
|instance_name|**sysname**|在部署 DAC 实例时指定的实例名称。|  
|type_name|**sysname**|在创建 DAC 包时指定的 DAC 的名称。|  
|type_version|**nvarchar(64)**|在创建 DAC 包时指定的 DAC 的版本。|  
|description|**nvarchar(4000)**|在创建 DAC 包时写入的 DAC 的说明。|  
|type_stream|**varbinary(max)**|包含在 DAC 中包含的逻辑对象（例如表和视图）的编码表示形式的位流。|  
|date_created|**datetime**|DAC 实例的创建日期和时间。|  
|created_by|**sysname**|创建了 DAC 实例的登录名。|  
  
## <a name="remarks"></a>备注  
 对此视图的只读访问可供有权连接到 master 数据库的所有用户。  
  
## <a name="permissions"></a>权限  
 要求具有 sysadmin 固定服务器角色的成员身份。  
  
## <a name="see-also"></a>请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
