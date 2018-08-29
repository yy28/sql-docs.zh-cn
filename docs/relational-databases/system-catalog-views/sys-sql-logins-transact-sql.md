---
title: sys.sql_logins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5740dbdf9961d0ab325b0fbfc023d4bd25045a08
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073457"
---
# <a name="syssqllogins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  为每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|--|继承自**sys.server_principals**。|  
|**is_policy_checked**|**bit**|检查密码策略。|  
|**is_expiration_checked**|**bit**|检查密码过期。|  
|**password_hash**|**varbinary(256)**|SQL 登录密码的哈希。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，存储的密码信息使用 SHA-512 加盐密码进行计算。|  
  
 此视图所继承的列的列表，请参阅[sys.server_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 若要查看这两个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录名和 Windows 身份验证登录名，请参阅[sys.server_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
 当包含启用的数据库用户时，可以不具有登录名建立连接。 若要标识这些帐户，请参阅[sys.database_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录都会显示各自的登录名称和 sa 登录信息。 要查看其他登录，需要获取 ALTER ANY LOGIN 或有关登录的权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [密码策略](../../relational-databases/security/password-policy.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
