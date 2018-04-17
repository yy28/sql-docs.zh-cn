---
title: dbo.sysproxies (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb17d288b1ca85adad9c686b550bfcdf68c90b73
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户的属性。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|代理帐户的 ID。|  
|**名称**|**sysname**|代理帐户的名称。|  
|**credential_id**|**int**|代理帐户使用的凭证的 ID。|  
|**enabled**|**tinyint**|代理帐户的状态。<br /><br /> **0** = 已禁用。 **1** = 启用。|  
|**说明**|**nvarchar(512)**|创建代理帐户时用户输入的说明。|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*的用户或组和代理凭据相关联。|  
|**credential_date_created**|**datetime**|凭证创建的日期和时间。|  
  
## <a name="remarks"></a>注释  
 只有的成员**sysadmin**固定的服务器角色可以访问**sysproxies**表。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysproxylogin &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
