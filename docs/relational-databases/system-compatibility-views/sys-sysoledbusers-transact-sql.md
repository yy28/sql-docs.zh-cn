---
title: sys.sysoledbusers (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 71d04ef07053eb893a98d654424eb49b61f0c7e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809135"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中包括此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统表只为了向后兼容。 我们建议你使用[目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)相反。  
  
 指定的链接服务器的每个用户和密码映射在表中对应一行。 **sysoledbusers**存储在**主**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|服务器的安全标识号 (SID)。|  
|**rmtloginame**|**nvarchar(** 128 **)**|远程登录名的**loginsid**映射到的链接**rmtservid**。|  
|**rmtpassword**|**nvarchar(** 128 **)**|返回 NULL。|  
|**loginsid**|**varbinary(** 85 **)**|要映射的本地登录 SID。|  
|**status**|**smallint**|如果为 1，则映射应使用用户凭据。|  
|**changedate**|**datetime**|最近更改映射信息的日期。|  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
