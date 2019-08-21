---
title: sp_cursorprepare (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b45ac37a4b2d8b37235bcf53164d6006c4ad51e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108424"
---
# <a name="sp_cursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将游标语句或批处理编译成执行计划，但并不创建游标。 编译的语句以后可供 sp_cursorexecute 使用。 此过程与 sp_cursorexecute 结合，具有相同的功能与 sp_cursoropen，但它拆分为两个阶段。 sp_cursorprepare 调用通过指定 ID = 3 在表格格式数据流 (TDS) 包中的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>参数  
 *prepared_handle*  
 SQL Server 生成准备好*处理*标识符，它返回一个整数值。  
  
> [!NOTE]  
>  *prepared_handle*随后将提供给 sp_cursorexecute 过程以打开游标。 一旦创建了句柄，它就一直存在，直到您注销或通过 sp_cursorunprepare 过程显式删除它。  
  
 *params*  
 标识参数化语句。 *Params*变量的定义替换为语句中的参数标记。 *params*是一个必需的参数，为调用**ntext**， **nchar**，或**nvarchar**输入值。 如果语句未参数化，则输入一个 NULL 值。  
  
> [!NOTE]  
>  使用**ntext**字符串作为输入值时*stmt*已参数化并*scrollopt* PARAMETERIZED_STMT 值为 ON。  
  
 *stmt*  
 定义游标结果集。 *Stmt*参数是必需的为调用**ntext**， **nchar**或者**nvarchar**输入值。  
  
> [!NOTE]  
>  指定的规则*stmt*值将与用于 sp_cursoropen，与异常相同的*stmt*字符串数据类型必须为**ntext**。  
  
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
  
 因为请求的值可能不适合于通过定义的游标*stmt*，此参数可同时用作输入和输出。 在此类情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分配一个适当的值。  
  
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
  
 如同*scrollpt*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以分配所请求不同的值。  
  
## <a name="remarks"></a>备注  
 RPC 状态参数为以下值之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|成功|  
|0x0001|失败|  
|1FF6|无法返回元数据。<br /><br /> 注意:这样做的原因是该语句不会生成一个结果集;例如，它是 INSERT 或 DDL 语句。|  
  
## <a name="examples"></a>示例  
 当*stmt*已参数化并*scrollopt* PARAMETERIZED_STMT 值为 ON，字符串的格式如下所示：  
  
 { *\<本地变量的名称 > \*\*\<数据类型 >* } [，...*n* ]  
  
## <a name="see-also"></a>请参阅  
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
