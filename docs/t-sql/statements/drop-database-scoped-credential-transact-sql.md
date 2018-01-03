---
title: "DROP DATABASE SCOPED CREDENTIAL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96016adf491a2869054068339a7fba64f8e7fedb
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="drop-database-scoped-credential-transact-sql"></a>DROP DATABASE SCOPED CREDENTIAL (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  从服务器中删除数据库范围的凭据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 是要从服务器中删除的数据库范围凭据的名称。  
  
## <a name="remarks"></a>Remarks  
 若要删除与数据库范围的凭据不删除数据库范围凭据本身相关联的密钥，使用[ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)。  
  
 有关数据库范围凭据的信息会显示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>权限  
 需要`ALTER`凭据的权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除名为的数据库范围凭据`SalesAccess`。  
  
```sql  
DROP DATABASE SCOPED CREDENTIAL AppCred;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [创建 DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
