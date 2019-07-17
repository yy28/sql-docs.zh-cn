---
title: sp_cursorprepexec (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c344948b5eab2de6c7987494a29fe1131c47f35a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108413"
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为提交的游标语句或批处理编译计划，然后创建并填充游标。 sp_cursorprepexec 结合了 sp_cursorprepare 和 sp_cursorexecute 的功能。 此过程通过在表格格式数据流 (TDS) 包中指定 ID = 5 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>参数  
 *准备的句柄*  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成准备*处理*标识符。 *准备的句柄*是必需的并返回**int**。  
  
 *cursor*  
 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的游标标识符。 *游标*是一个必需的参数，必须提供对此游标，如 sp_cursorfetch 执行操作的所有后续过程。  
  
 *params*  
 标识参数化语句。 *Params*变量的定义替换为语句中的参数标记。 *params*是一个必需的参数，为调用**ntext**， **nchar**，或**nvarchar**输入值。  
  
> [!NOTE]  
>  使用**ntext**字符串作为输入值时*stmt*已参数化并*scrollopt* PARAMETERIZED_STMT 值为 ON。  
  
 *语句*  
 定义游标结果集。 *语句*参数是必需的为调用**ntext**， **nchar**或者**nvarchar**输入值。  
  
> [!NOTE]  
>  用于指定 stmt 值的规则是与用于 sp_cursoropen，与异常相同的*stmt*必须是字符串数据类型**ntext**。  
  
 *options*  
 一个可选参数，它返回游标结果集列的说明。 *选项*需要如下**int**输入值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 滚动选项。 *scrollopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 由于可能存在的请求的选项不适合于通过定义的游标 *\<stmt >* ，此参数可同时用作输入和输出。 在此类情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分配一个适当的类型并修改此值。  
  
 *ccopt*  
 并发控制选项。 *ccopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS（以前称为 LOCKCC）|  
|0x0004|**乐观**（以前称为 OPTCC）|  
|0x0008|OPTIMISTIC（以前称为 OPTCCVAL）|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同*scrollpt*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以分配与所请求不同的值。  
  
 *rowcount*  
 一个可选参数，指示要用于 AUTO_FETCH 的提取缓冲区行数。 默认值为 20 行。 *行计数*以不同的方式指定为输入值与返回值时的行为。  
  
|作为输入值|作为返回值|  
|--------------------|---------------------|  
|当使用 FAST_FORWARD 游标指定 AUTO_FETCH 时*rowcount*表示要放入提取缓冲区的行数。|表示结果集中的行数。 当*scrollopt*指定 AUTO_FETCH 值，则*rowcount*返回提取到提取缓冲区的行数。|  
  
## <a name="return-code-values"></a>返回代码值  
 如果*params*返回 NULL 值，则该语句未参数化。  
  
## <a name="see-also"></a>请参阅  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
