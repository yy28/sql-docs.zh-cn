---
title: "ERROR_MESSAGE (Transact SQL) |Microsoft 文档"
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
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f15d9d23726f7558f0bf73aff3f8c3c5253cb24d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回导致 TRY…CATCH 构造的 CATCH 块运行的错误的消息文本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>返回值  
 在 CATCH 块中调用时，返回导致 CATCH 块运行的错误消息的完整文本。 该文本包括为所有可替换参数提供的值，如长度、对象名或时间。  
  
 如果在 CATCH 块作用域以外调用，则返回 NULL。  
  
## <a name="remarks"></a>注释  
 ERROR_MESSAGE 可以在 CATCH 块作用域内的任意位置调用。  
  
 ERROR_MESSAGE 无论运行多少次，无论在 CATCH 块作用域内的什么位置运行，它都返回错误消息。 这是相反功能，例如 @@ERROR、 其只返回立即后导致的错误的一个语句中的错误号或 CATCH 的第一个语句块。  
  
 在嵌套 CATCH 块中，ERROR_MESSAGE 返回特定于它被引用 CATCH 块作用域的错误消息。 例如，外部 TRY...CATCH 构造的 CATCH 块可能具有嵌套 TRY...CATCH 构造。 在嵌套 CATCH 块中，ERROR_MESSAGE 返回调用该嵌套 CATCH 块的错误消息。 如果 ERROR_MESSAGE 在外部 CATCH 块中运行，它将返回调用该外部 CATCH 块的错误消息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. 在 CATCH 块中使用 ERROR_MESSAGE  
 下面的代码示例显示生成被零除错误的 `SELECT` 语句。 将返回错误消息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. 在 CATCH 块中将 ERROR_MESSAGE 与其他错误处理工具一起使用  
 下面的代码示例显示生成被零除错误的 `SELECT` 语句。 同时返回错误消息和有关错误的信息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block"></a>C. 在 CATCH 块中使用 ERROR_MESSAGE  
 下面的代码示例显示生成被零除错误的 `SELECT` 语句。 将返回错误消息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>D. 在 CATCH 块中将 ERROR_MESSAGE 与其他错误处理工具一起使用  
 下面的代码示例显示生成被零除错误的 `SELECT` 语句。 同时返回错误消息和有关错误的信息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.messages (Transact-SQL)](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE (Transact-SQL)](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_NUMBER (Transact-SQL)](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE (Transact-SQL)](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR (Transact-SQL)](../../t-sql/functions/error-transact-sql.md)  
  
  


