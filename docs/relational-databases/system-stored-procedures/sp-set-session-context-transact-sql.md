---
title: sp_set_session_context (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1396ef79eb69b96a40f075c50cd38b6ad77d24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

设置此会话上下文中的键 / 值对。  
  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_set_session_context [ @key= ] 'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 [ @key=] key  
 正在设置的类型的密钥**sysname**。 最大密钥大小是 128 个字节。  
  
 [ @value=] 'value'  
 类型的指定键的值**sql_variant**。 设置的值为 NULL 释放的内存。 最大大小为 8,000 个字节。  
  
 [ @read_only= ] { 0 | 1 }  
 类型的标志**位**。 如果为 1，然后指定键的值无法再次更改此逻辑连接。 如果可以更改 0 （默认值），则值。  
  
## <a name="permissions"></a>权限  
 任何用户可以为其会话设置会话上下文。  
  
## <a name="remarks"></a>注释  
 与其他存储过程一样可以作为参数传递仅文本和变量 （不表达式或函数调用）。  
  
 会话上下文的总大小被限制为 256 kb。 如果一个值，导致超过此限制的组，该语句将失败。 你可以监视中的总体内存使用情况[sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)。  
  
 你可以通过查询监视总体内存使用情况[sys.dm_os_memory_cache_counters &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) ，如下所示： `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>示例  
 下面的示例演示如何设置，然后返回名为值为英语语言的会话上下文项。  
  
```  
EXEC sp_set_session_context 'language', 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 下面的示例演示如何使用可选的只读标志。  
  
```  
EXEC sp_set_session_context 'user_id', 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CURRENT_TRANSACTION_ID (Transact-SQL)](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT (Transact-SQL)](../../t-sql/functions/session-context-transact-sql.md)   
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO (Transact-SQL)](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO (Transact-SQL)](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
