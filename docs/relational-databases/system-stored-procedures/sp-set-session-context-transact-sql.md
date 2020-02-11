---
title: sp_set_session_context （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a57bf4acff6f8d0d08f86852de5ecc0411211c67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104395"
---
# <a name="sp_set_session_context-transact-sql"></a>sp_set_session_context （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

在会话上下文中设置键值对。  
  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 [ @key= ]N'key'  
 要设置的键，类型为**sysname**。 最大密钥大小为128个字节。  
  
 [ @value= ]负值  
 **Sql_variant**类型的指定键的值。 如果将值设置为 NULL，则释放内存。 最大大小为 8,000 个字节。  
  
 [ @read_only= ]{0 | 1}  
 类型**位**的标志。 如果为1，则无法在此逻辑连接上再次更改指定键的值。 如果为0（默认值），则该值可以更改。  
  
## <a name="permissions"></a>权限  
 任何用户都可以为其会话设置会话上下文。  
  
## <a name="remarks"></a>备注  
 与其他存储过程一样，只有文本和变量（而不是表达式或函数调用）可以作为参数传递。  
  
 会话上下文的总大小限制为 1 MB。 如果设置的值导致超过此限制，则语句将失败。 可以监视[sys.databases&#41;dm_os_memory_objects &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)的总体内存使用情况。  
  
 可以通过按如下所示 dm_os_memory_cache_counters 查询[&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)来监视总体内存使用情况：`SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>示例  
 下面的示例演示如何设置并返回值为英语的名为 language 的会话上下文键。  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 下面的示例演示如何使用可选的只读标志。  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CURRENT_TRANSACTION_ID (Transact-SQL)](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-sql&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO (Transact-SQL)](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO (Transact-SQL)](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
