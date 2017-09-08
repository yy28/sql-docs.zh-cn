---
title: "SET CONTEXT_INFO (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f74a45830a295467552c8fdc9f4781260339d9a6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将最多 128 字节的二进制信息与当前会话或连接关联。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>参数  
 *binary_str*  
 是**二进制**常量或隐式转换为一个常数**二进制**、 要与当前会话或连接关联。  
  
 **@***binary_var*  
 是**varbinary**或**二进制**保存某上下文的值要与当前会话或连接关联的变量。  
  
## <a name="remarks"></a>注释  
 检索当前会话的上下文信息的首选方式是使用 CONTEXT_INFO 函数。 会话上下文信息也存储在**context_info**以下系统视图中的列：  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 不能在用户定义函数中指定 SET CONTEXT_INFO。 不能向 SET CONTEXT_INFO 提供一个 NULL 值，因为保存值的视图不允许使用 NULL 值。  
  
 SET CONTEXT_INFO 不接受常量名或变量名以外的表达式。 若要设置的上下文信息为函数调用的结果，必须首先包含中的函数调用的结果**二进制**或**varbinary**变量。  
  
 与其他 SET 语句不同，在存储过程或触发器中发出 SET CONTEXT_INFO 时，为上下文信息设置的新值在存储过程或触发器完成后会继续存在。  
  
## <a name="examples"></a>示例  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. 使用常量设置上下文信息  
 以下示例通过设置值并显示结果来阐释 `SET CONTEXT_INFO`。 请注意，查询 `sys.dm_exec_sessions` 要求 SELECT 和 VIEW SERVER STATE 权限，但使用 CONTEXT_INFO 函数则不需要。  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. 使用函数设置上下文信息  
 下面的示例演示了如何使用函数的输出设置上下文值，其中的值从函数必须先将放在**二进制**变量。  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40;Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  

