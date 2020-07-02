---
title: dbo.sys代理（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e49698ae6692a06c141a4182df3c54cd4f61d43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750301"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户的属性。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|代理帐户的 ID。|  
|name|**sysname**|代理帐户的名称。|  
|**credential_id**|**int**|代理帐户使用的凭证的 ID。|  
|**能够**|**tinyint**|代理帐户的状态。<br /><br /> **0** = 禁用。 **1** = 已启用。|  
|**2008**|**nvarchar(512)**|创建代理帐户时用户输入的说明。|  
|**user_sid**|**varbinary （85）**|与代理凭据关联的用户或组的 Microsoft Windows *security_identifier* 。|  
|**credential_date_created**|**datetime**|凭证创建的日期和时间。|  
  
## <a name="remarks"></a>备注  
 只有**sysadmin**固定服务器角色的成员才能访问**sysproxies**表。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysproxylogin &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sys子系统 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
