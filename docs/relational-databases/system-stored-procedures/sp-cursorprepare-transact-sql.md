---
title: sp_cursorprepare (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1134a3edbbbf1a838207a122e43bbafb5ac0e18b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将游标语句或批处理编译成执行计划，但并不创建游标。 编译的语句以后可供 sp_cursorexecute 使用。 此过程中，结合了 sp_cursorexecute，具有与 sp_cursoropen，相同的功能，但拆分为两个阶段。 通过指定 ID 调用 sp_cursorprepare = 表格格式数据流 (TDS) 数据包中的 3。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>参数  
 *prepared_handle*  
 SQL Server 生成已准备好*处理*返回一个整数值的标识符。  
  
> [!NOTE]  
>  *prepared_handle*才能打开游标随后提供给 sp_cursorexecute 过程。 一旦创建了句柄，它就一直存在，直到您注销或通过 sp_cursorunprepare 过程显式删除它。  
  
 *params*  
 标识参数化语句。 *Params*的变量的定义替换为在语句中的参数标记。 *params*是必需的参数来调用**ntext**， **nchar**，或**nvarchar**输入值。 如果语句未参数化，则输入一个 NULL 值。  
  
> [!NOTE]  
>  使用**ntext**作为输入的字符串值时*stmt*进行参数化和*scrollopt* PARAMETERIZED_STMT 值为 ON。  
  
 *stmt*  
 定义游标结果集。 *Stmt*参数是必需的调用**ntext**， **nchar**或**nvarchar**输入值。  
  
> [!NOTE]  
>  指定的规则*stmt*值是否不同于为 sp_cursoropen，出现异常， *stmt*字符串数据类型必须为**ntext**。  
  
 *options*  
 一个可选参数，它返回游标结果集列的说明。 *选项*需要具备以下**int**输入值。  
  
|“值”|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 滚动选项。 *scrollopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|“值”|Description|  
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
  
 由于请求的值可能不是适用于由定义光标*stmt*，此参数提供为这两个输入和输出。 在此类情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分配一个适当的值。  
  
 *ccopt*  
 并发控制选项。 *ccopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|“值”|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS（以前称为 LOCKCC）|  
|0x0004|**开放式**（以前称为 OPTCC）|  
|0x0008|OPTIMISTIC（以前称为 OPTCCVAL）|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 与*scrollpt*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以分配请求的一个不同的值。  
  
## <a name="remarks"></a>注释  
 RPC 状态参数为以下值之一：  
  
|“值”|说明|  
|-----------|-----------------|  
|0|成功|  
|0x0001|失败|  
|1FF6|无法返回元数据。<br /><br /> 注意： 这的原因是该语句不会生成结果集;例如，它是 INSERT 或 DDL 语句。|  
  
## <a name="examples"></a>示例  
 当*stmt*进行参数化和*scrollopt* PARAMETERIZED_STMT 值为 ON，字符串的格式为，如下所示：  
  
 { *\<本地变量的名称 > * *\<数据类型 >* } [，...*n* ]  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursorexecute &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
