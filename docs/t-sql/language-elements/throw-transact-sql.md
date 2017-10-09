---
title: "THROW (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- THROW_TSQL
- THROW
dev_langs:
- TSQL
helpviewer_keywords:
- THROW statement
ms.assetid: 43661b89-8f13-4480-ad53-70306cbb14c5
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e61cb9edc75dda4368e31e9eac6e4e452d4387f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="throw-transact-sql"></a>THROW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  引发异常，并将执行转移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中 TRY…CATCH 构造的 CATCH 块。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
THROW [ { error_number | @local_variable },  
        { message | @local_variable },  
        { state | @local_variable } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *error_number*  
 表示异常的常量或变量。 *error_number*是**int**并且必须为大于或等于 50000 且小于或等于 2147483647。  
  
 *消息*  
 描述异常的字符串或变量。 *消息*是**nvarchar(2048)**。  
  
 *状态*  
 在 0 到 255 之间的常量或变量，指示与消息关联的状态。 *状态*是**tinyint**。  
  
## <a name="remarks"></a>注释  
 THROW 语句前的语句必须后跟分号 (;) 语句终止符。  
  
 如果 TRY…CATCH 构造不可用，则会话结束。 设置引发异常的行号和过程。 将严重性设置为 16。  
  
 如果指定 THROW 语句时未使用任何参数，该语句必须出现在 CATCH 块内。 这将导致引发已捕获异常。 THROW 语句中出现任何错误将导致语句批处理结束状态。  
  
 % 是 THROW 语句的消息文本中的保留的字符，必须对其进行转义。 重复 % 字符以将 % 作为消息文本的一部分返回，例如“增加超出了 15%% 的原始值”。  
  
## <a name="differences-between-raiserror-and-throw"></a>RAISERROR 与 THROW 之间的差异  
 下表列出了 RAISERROR 和 THROW 语句之间的一些差异。  
  
|RAISERROR 语句|THROW 语句|  
|-------------------------|---------------------|  
|如果*msg_id*传递到 RAISERROR，必须在 sys.messages 中定义的 ID。|*Error_number*参数无需在 sys.messages 中定义。|  
|*Msg_str*参数可以包含**printf**格式设置样式。|*消息*参数不接受**printf**样式的格式设置。|  
|*严重性*参数指定的异常的严重性。|没有任何*严重性*参数。 始终将异常严重性设置为 16。|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-throw-to-raise-an-exception"></a>A. 使用 THROW 引发异常  
 下面的示例演示如何使用`THROW`语句来引发异常。  
  
```tsql  
THROW 51000, 'The record does not exist.', 1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 51000, Level 16, State 1, Line 1  
  
 The record does not exist.
 ```  
  
### <a name="b-using-throw-to-raise-an-exception-again"></a>B. 使用 THROW 再次引发异常  
 以下示例演示如何使用 `THROW` 语句再次引发上次引发的异常。  
  
```tsql  
USE tempdb;  
GO  
CREATE TABLE dbo.TestRethrow  
(    ID INT PRIMARY KEY  
);  
BEGIN TRY  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
--  Force error 2627, Violation of PRIMARY KEY constraint to be raised.  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
END TRY  
BEGIN CATCH  
  
    PRINT 'In catch block.';  
    THROW;  
END CATCH;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 PRINT 'In catch block.';  
 Msg 2627, Level 14, State 1, Line 1  
 Violation of PRIMARY KEY constraint 'PK__TestReth__3214EC272E3BD7D3'. Cannot insert duplicate key in object 'dbo.TestRethrow'.  
 The statement has been terminated.
 ```  
  
### <a name="c-using-formatmessage-with-throw"></a>C. 使用带 THROW 的 FORMATMESSAGE  
 下面的示例说明如何使用带 `FORMATMESSAGE` 的 `THROW` 函数来引发自定义错误消息。 该示例首先使用 `sp_addmessage` 创建用户定义的错误消息。 因为 THROW 语句不允许替换中的参数*消息*方式 RAISERROR 执行，而 FORMATMESSAGE 函数的参数用于传递错误消息 60000 所需的三个参数值。  
  
```tsql  
EXEC sys.sp_addmessage  
     @msgnum   = 60000  
,@severity = 16  
,@msgtext  = N'This is a test message with one numeric parameter (%d), one string parameter (%s), and another string parameter (%s).'  
    ,@lang = 'us_english';   
GO  
  
DECLARE @msg NVARCHAR(2048) = FORMATMESSAGE(60000, 500, N'First string', N'second string');   
  
THROW 60000, @msg, 1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 60000, Level 16, State 1, Line 2  
 This is a test message with one numeric parameter (500), one string parameter (First string), and another string parameter (second string).
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-throw-to-raise-an-exception"></a>D. 使用 THROW 引发异常  
 下面的示例演示如何使用`THROW`语句来引发异常。  
  
```tsql  
THROW 51000, 'The record does not exist.', 1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 51000, Level 16, State 1, Line 1  
  
 The record does not exist.
 ```  
  
## <a name="see-also"></a>另请参阅  
 [FORMATMESSAGE &#40;Transact SQL &#41;](../../t-sql/functions/formatmessage-transact-sql.md)   
 [数据库引擎错误严重性](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE (Transact-SQL)](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE (Transact-SQL)](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER (Transact-SQL)](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE (Transact-SQL)](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR (Transact-SQL)](../../t-sql/functions/error-transact-sql.md)   
 [转到 &#40;Transact SQL &#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [开始...结束 &#40;Transact SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40;Transact SQL &#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [设置 XACT_ABORT &#40;Transact SQL &#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  


