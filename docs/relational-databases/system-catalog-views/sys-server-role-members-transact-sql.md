---
title: sys.server_role_members (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_role_members
- sys.server_role_members_TSQL
- server_role_members_TSQL
- sys.server_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_role_members catalog view
ms.assetid: efa20414-2c6b-45a2-a7a9-60110a24da18
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4107e6c1f675f7fae78ca384c082ef12c2fa309b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743939"
---
# <a name="sysserverrolemembers-transact-sql"></a>sys.server_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  为每个固定和用户定义的服务器角色的每个成员返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|角色的服务器主体 ID。|  
|**member_principal_id**|**int**|成员的服务器主体 ID。|  
  
 若要添加或删除服务器角色成员身份，使用[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)语句。  
  
## <a name="permissions"></a>权限  
 登录名可以查看他们自己的服务器角色成员身份，可以查看的固定的服务器角色的成员的 principal_id。 若要查看所有服务器角色成员身份，需要**都视图 DEFINITION ON SERVER ROLE**权限或成员身份**securityadmin**固定的服务器角色。  
  
 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
 下面的示例返回角色和其成员的名称和 ID。  
  
```  
SELECT sys.server_role_members.role_principal_id, role.name AS RoleName,   
    sys.server_role_members.member_principal_id, member.name AS MemberName  
FROM sys.server_role_members  
JOIN sys.server_principals AS role  
    ON sys.server_role_members.role_principal_id = role.principal_id  
JOIN sys.server_principals AS member  
    ON sys.server_role_members.member_principal_id = member.principal_id;  
```  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [服务器级别角色](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
