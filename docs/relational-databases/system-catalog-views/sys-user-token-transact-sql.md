---
title: "sys.user_token (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs: TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6c552b797a78fe27b0a6b4253ad44aee37b8f67
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysusertoken-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中组成用户标记的每个数据库主体返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|主体的 ID。 该值在数据库中是唯一的。|  
|**sid**|**varbinary(85)**|如果主体数据库在数据库之外定义，则为主体数据库的安全标识符。 例如，它可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录、Windows 登录、Windows 组登录或映射到证书的登录，否则，该值为 NULL。|  
|**名称**|**nvarchar (128)**|主体名称。 该值在数据库中是唯一的。|  
|**type**|**nvarchar (128)**|主体类型的说明。 所有类型都映射到**sid**。 该值可以是下列值之一：<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**使用情况**|**nvarchar (128)**|指示服务器主体参与 GRANT 或 DENY 权限的鉴定，或用作验证器。<br /><br /> 此值可以为下列值之一：<br /><br /> GRANT 或 DENY<br /><br /> 仅 DENY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>另请参阅  
 [sys.login_token &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
