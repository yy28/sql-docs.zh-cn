---
title: sys.login_token (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 62cc40af6ebf3df276f2c0aa3a81eb6703f68c39
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021435"
---
# <a name="syslogintoken-transact-sql"></a>sys.login_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为登录名标记中包含的每个服务器主体返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|主体的 ID。 此值在服务器中是唯一的。|  
|**sid**|**varbinary(85)**|服务器主体的安全标识符。 如果这是 Windows 主体**sid** = Windows SID。 如果该登录名映射到证书，请**sid** = 从证书的 GUID。|  
|**名称**|**nvarchar(128)**|主体的名称。 此值在服务器中是唯一的。|  
|**类型**|**nvarchar(128)**|主体类型的说明。 所有类型都映射到**sid**。 该值可以是下列值之一：<br /><br /> SQL LOGIN<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> LOGIN MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**使用情况**|**nvarchar(128)**|指示服务器主体参与 GRANT 或 DENY 权限的鉴定，或用作验证器。<br /><br /> 此值可以为下列值之一：<br /><br /> GRANT 或 DENY<br /><br /> 仅 DENY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>请参阅  
 [sys.user_token &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
