---
title: 安全函数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], security
- security functions
- roles [SQL Server], functions
- users [SQL Server], security functions
- security [SQL Server], functions
ms.assetid: 7773a87d-2f1b-4951-a225-baf159a7291b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a1e360bd23b7fc1b32dd29da85fc9edb5d8d841
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="security-functions-transact-sql"></a>安全函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列函数返回对管理安全性有用的信息。 其他函数在[加密函数 (Transact-SQL)](../../t-sql/functions/cryptographic-functions-transact-sql.md) 下列出。  
  
|||  
|-|-|  
|[CERTENCODED (Transact-SQL)](../../t-sql/functions/certencoded-transact-sql.md)|[PWDCOMPARE (Transact-SQL)](../../t-sql/functions/pwdcompare-transact-sql.md)|  
|[CERTPRIVATEKEY (Transact-SQL)](../../t-sql/functions/certprivatekey-transact-sql.md)|[PWDENCRYPT (Transact-SQL)](../../t-sql/functions/pwdencrypt-transact-sql.md)|  
|[CURRENT_USER (Transact-SQL)](../../t-sql/functions/current-user-transact-sql.md)|[SCHEMA_ID (Transact-SQL)](../../t-sql/functions/schema-id-transact-sql.md)|  
|[DATABASE_PRINCIPAL_ID (Transact-SQL)](../../t-sql/functions/database-principal-id-transact-sql.md)|[SCHEMA_NAME (Transact-SQL)](../../t-sql/functions/schema-name-transact-sql.md)|  
|[sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)|[SESSION_USER (Transact-SQL)](../../t-sql/functions/session-user-transact-sql.md)|  
|[sys.fn_get_audit_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)|[SUSER_ID (Transact-SQL)](../../t-sql/functions/suser-id-transact-sql.md)|  
|[sys.fn_my_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)|[SUSER_SID (Transact-SQL)](../../t-sql/functions/suser-sid-transact-sql.md)|  
|[HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)|[SUSER_SNAME (Transact-SQL)](../../t-sql/functions/suser-sname-transact-sql.md)|  
|[IS_MEMBER (Transact-SQL)](../../t-sql/functions/is-member-transact-sql.md)|[SYSTEM_USER (Transact-SQL)](../../t-sql/functions/system-user-transact-sql.md)|  
|[IS_ROLEMEMBER (Transact-SQL)](../../t-sql/functions/is-rolemember-transact-sql.md)|[SUSER_NAME (Transact-SQL)](../../t-sql/functions/suser-name-transact-sql.md)|  
|[IS_SRVROLEMEMBER (Transact-SQL)](../../t-sql/functions/is-srvrolemember-transact-sql.md)|[USER_ID (Transact-SQL)](../../t-sql/functions/user-id-transact-sql.md)|  
|[ORIGINAL_LOGIN (Transact-SQL)](../../t-sql/functions/original-login-transact-sql.md)|[USER_NAME (Transact-SQL)](../../t-sql/functions/user-name-transact-sql.md)|  
|[PERMISSIONS (Transact-SQL)](../../t-sql/functions/permissions-transact-sql.md)||  
  
 有关 Windows 组中成员身份的信息，请参阅 [xp_logininfo (Transact-SQL)](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md) 和 [xp_enumgroups (Transact-SQL)](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [加密函数 (Transact-SQL)](../../t-sql/functions/cryptographic-functions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [安全语句](http://msdn.microsoft.com/library/aebe2ec7-31bc-4697-a493-dcfcd0903a7b)  
  
  
