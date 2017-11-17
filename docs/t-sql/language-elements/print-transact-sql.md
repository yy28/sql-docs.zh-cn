---
title: "打印 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: a1044fb78ebf3852a963d11607433fdb93d48007
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="print-transact-sql"></a>打印 Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  向客户端返回用户定义消息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>参数  
 *msg_str*  
 字符串或 Unicode 字符串常量。 有关详细信息，请参阅[常量 &#40;Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***local_variable*  
 任何有效的字符数据类型的变量。 **@***local_variable*必须**char**， **nchar**， **varchar**，或**nvarchar**，或它必须能够隐式转换为这些数据类型。  
  
 *string_expr*  
 返回字符串的表达式。 可包括串联的文字值、函数和变量。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 如果消息字符串为非 Unicode 字符串，则最长不得超过 8,000 个字符；如果消息字符串为 Unicode 字符串，则最长不得超过 4,000 个字符。 超过最大长度的字符串会被截断。 **Varchar （max)**和**nvarchar (max)**数据类型被截断为数据类型都不大于**varchar （8000)**和**nvarchar （4000)**.  
  
 RAISERROR 也可以用于返回消息。 RAISERROR 与 PRINT 相比具有以下优点：  
  
-   RAISERROR 支持使用 C 语言标准库 printf 函数上的建模机制将参数代入错误消息字符串。  
  
-   除了文本消息，RAISERROR 还可以指定唯一错误编号、严重性和状态代码。  
  
-   RAISERROR 可用于返回使用 sp_addmessage 系统存储过程创建的用户定义的消息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. 有条件地执行输出 (IF EXISTS)  
 以下示例使用 `PRINT` 语句有条件地返回消息。  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. 生成并显示字符串  
 以下示例将 `GETDATE` 函数的结果转换为 `nvarchar` 数据类型，并将其与 `PRINT` 要返回的文本串联。  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. 有条件地执行打印  
 以下示例使用 `PRINT` 语句有条件地返回消息。  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40;Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  


