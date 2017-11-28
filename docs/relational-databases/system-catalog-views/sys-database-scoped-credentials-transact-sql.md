---
title: "sys.database_scoped_credentials (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords: sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
caps.latest.revision: "2"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34db44a8b28ef9441e9bd6214e89ba2ef0e9f41b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>sys.database_scoped_credentials (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回一个行，每个数据库范围的数据库中的凭据。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|数据库范围凭据的 ID。 是在数据库中唯一的。|  
|name|**sysname**|数据库的名称范围的凭据。 是在数据库中唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用的标识的名称。 这通常是一个 Windows 用户。 它不必是唯一的。|  
|create_date|**datetime**|在其中创建数据库范围凭据的时间。|  
|modify_date|**datetime**|数据库范围凭据的上次修改时间。|  
|target_type|**nvarchar(100)**|类型的数据库范围的凭据。 返回`NULL`数据库范围的凭据。|  
|target_id|**int**|数据库范围凭据映射到的对象 ID。 数据库，则返回 0 范围的凭据|  
  
## <a name="permissions"></a>Permissions  
 需要对数据库拥有 `CONTROL` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [创建 DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
