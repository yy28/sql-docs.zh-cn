---
title: "SESSION_CONTEXT (TRANSACT-SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23eea4b51009272ae06987ee2e9c1730750b3d6d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回当前会话上下文中指定的键的值。 该数值将通过使用[sp_set_session_context &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>参数  
 key  
 正在检索的值的键 (sysname 类型)。  
  
## <a name="return-type"></a>返回类型  
 **sql_variant**  
  
## <a name="return-value"></a>返回值  
 如果已为该注册表项不设置任何值与中的会话上下文或为 NULL 的指定键关联的值。  
  
## <a name="permissions"></a>Permissions  
 任何用户可以读取其会话的会话上下文。  
  
## <a name="remarks"></a>注释  
 SESSION_CONTEXT 的 MARS 行为是类似于 CONTEXT_INFO。 如果在 MARS 批处理设置键 / 值对，新值将不会以返回其他 MARS 批处理同一个连接上除非它们启动后设置新值的批处理已完成。 如果多个 MARS 批处理上处于活动状态的连接，无法将值设置为"read_only。" 这样可以防止争用条件和非确定性有关的值"wins"。  
  
## <a name="examples"></a>示例  
 下面的简单示例设置键的会话上下文值`user_id`到 4，然后使用**SESSION_CONTEXT**函数以检索值。  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_set_session_context (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [设置 CONTEXT_INFO &#40;Transact SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  

