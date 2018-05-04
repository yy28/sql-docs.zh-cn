---
title: sp_databases (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c9f60f43f2fb26b1e166770f3f0e5b923ef4937a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spdatabases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出驻留在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中的数据库或可以通过数据库网关访问的数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|数据库的名称。 在[!INCLUDE[ssDE](../../includes/ssde-md.md)]，此列表示的数据库名称，如存储在**sys.databases**目录视图。|  
|**DATABASE_SIZE**|**int**|数据库的大小（以 KB 计）。|  
|**备注**|**varchar(254)**|对于[!INCLUDE[ssDE](../../includes/ssde-md.md)]，此字段始终返回 NULL。|  
  
## <a name="remarks"></a>注释  
 所返回的数据库名称可以作为 USE 语句的参数，用来更改当前数据库上下文。  
  
 **sp_databases**具有开放式数据库连接 (ODBC) 的无等效项。  
  
## <a name="permissions"></a>权限  
 需要 CREATE DATABASE 或 ALTER ANY DATABASE 或 VIEW ANY DEFINITION 权限，并且必须有该数据库的访问权。 不能是被拒绝的 VIEW ANY DEFINITION 权限。  
  
## <a name="examples"></a>示例  
 以下示例显示如何执行 `sp_databases`。  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;Transact SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
