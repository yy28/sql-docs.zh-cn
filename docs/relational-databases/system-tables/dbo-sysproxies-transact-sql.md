---
title: dbo.sysproxies (Transact SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a37300ad1bf16ac76fbcbd0c6e77870077f7f631
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846405"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户的属性。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|代理帐户的 ID。|  
|**名称**|**sysname**|代理帐户的名称。|  
|**credential_id**|**int**|代理帐户使用的凭证的 ID。|  
|**enabled**|**tinyint**|代理帐户的状态。<br /><br /> **0** = 已禁用。 **1** = 启用。|  
|**description**|**nvarchar(512)**|创建代理帐户时用户输入的说明。|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*的用户或组和代理服务器凭据相关联。|  
|**credential_date_created**|**datetime**|凭证创建的日期和时间。|  
  
## <a name="remarks"></a>备注  
 只有的成员**sysadmin**固定的服务器角色可以访问**sysproxies**表。  
  
## <a name="see-also"></a>请参阅  
 [dbo.sysproxylogin &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
