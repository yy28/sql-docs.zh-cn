---
title: sys.database_credentials (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords:
- sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 88ec73b3c29dfa8d9db0d4322b34b08ac535a621
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180203"
---
# <a name="sysdatabasecredentials-transact-sql"></a>sys.database_credentials (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回一个行，每个数据库范围的数据库中的凭据。  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)相反。    
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|数据库范围凭据的 ID。 是在数据库中唯一的。|  
|name|**sysname**|数据库的名称范围的凭据。 是在数据库中唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用的标识的名称。 这通常是一个 Windows 用户。 它不必是唯一的。|  
|create_date|**datetime**|在其中创建数据库范围凭据的时间。|  
|modify_date|**datetime**|数据库范围凭据的上次修改时间。|  
|target_type|**nvarchar(100)**|类型的数据库范围的凭据。 返回 NULL 数据库范围的凭据。|  
|target_id|**int**|数据库范围凭据映射到的对象 ID。 数据库，则返回 0 范围的凭据|  
  
## <a name="permissions"></a>权限  
 需要对数据库拥有 `CONTROL` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
