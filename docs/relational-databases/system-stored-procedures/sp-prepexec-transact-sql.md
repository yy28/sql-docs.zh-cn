---
title: "sp_prepexec (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fccac9582efdd54c5af023b721bbf868bcc38980
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spprepexec-transact-sql"></a>sp_prepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  准备并执行参数化[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 sp_prepexec 将合并 sp_prepare 和 sp_execute 的功能。 这通过在表格格式数据流 (TDS) 包中指定 ID =13 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>参数  
 *句柄*  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-生成*处理*标识符。 *处理*为所需的参数且具有**int**返回值。  
  
 *params*  
 标识参数化语句。 *Params*的变量的定义替换为在语句中的参数标记。 *params*是必需的参数来调用**ntext**， **nchar**，或**nvarchar**输入值。 如果语句未参数化，则输入一个 NULL 值。  
  
 *stmt*  
 定义游标结果集。 *Stmt*参数是必需的调用**ntext**， **nchar**或**nvarchar**输入值。  
  
 *bound_param*  
 指示可选使用其他参数。 *bound_param*调用的任何数据类型指定在使用的附加参数的输入值。  
  
## <a name="examples"></a>示例  
 下面的示例准备并执行一个简单的语句。  
  
```  
Declare @P1 int;  
EXEC sp_prepexec @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
@P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @P1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_prepare &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
