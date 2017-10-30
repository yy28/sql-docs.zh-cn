---
title: "ERROR_PROCEDURE (Transact SQL) |Microsoft 文档"
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
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5bd076bd3ee690d834c27f37544b8fd4ab6402
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回发生错误而导致运行 TRY…CATCH 构造的 CATCH 块的存储过程或触发器的名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar （128)**  
  
## <a name="return-value"></a>返回值  
 在 CATCH 块中调用时，返回出现错误的存储过程名称。  
  
 如果该错误未在存储过程或触发器中出现，则返回 NULL。  
  
 如果在 CATCH 块作用域以外调用，则返回 NULL。  
  
## <a name="remarks"></a>注释  
 ERROR_PROCEDURE 可以在 CATCH 块的作用域内的任何位置调用。  
  
 ERROR_PROCEDURE 返回出现错误的存储过程或触发器的名称，无论它被调用多少次或在 CATCH 块的作用域的哪个位置被调用。 这形成了鲜明对比与函数，如@ERROR，其返回的错误号，紧跟导致错误的一个语句中或在 CATCH 块的第一个语句。  
  
 在嵌套的 CATCH 块中，ERROR_PROCEDURE 返回存储过程或触发器的名称，该存储过程或触发器与在其中引用它的 CATCH 块的作用域是特定相关的。 例如，TRY…CATCH 构造的 CATCH 块可以有嵌套的 TRY…CATCH。 在嵌套的 CATCH 块中，ERROR_PROCEDURE 返回调用嵌套 CATCH 块的出错的存储过程或触发器的名称。 如果 ERROR_PROCEDURE 在 CATCH 块之外运行，它将返回调用该 CATCH 块的出错的存储过程或触发器的名称。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>A. 在 CATCH 块中使用 ERROR_PROCEDURE  
 下面的代码示例显示了一个会生成被零除错误的存储过程。 `ERROR_PROCEDURE` 返回发生错误的存储过程的名称。  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>B. 通过其他错误处理工具在 CATCH 块中使用 ERROR_PROCEDURE。  
 下面的代码示例显示了一个会生成被零除错误的存储过程。 与该错误相关的信息连同出错的存储过程的名称一起返回。  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorprocedure-in-a-catch-block"></a>C. 在 CATCH 块中使用 ERROR_PROCEDURE  
 下面的代码示例显示了一个会生成被零除错误的存储过程。 `ERROR_PROCEDURE` 返回发生错误的存储过程的名称。  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>D. 通过其他错误处理工具在 CATCH 块中使用 ERROR_PROCEDURE。  
 下面的代码示例显示了一个会生成被零除错误的存储过程。 与该错误相关的信息连同出错的存储过程的名称一起返回。  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
        END CATCH;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.messages (Transact-SQL)](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE (Transact-SQL)](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE (Transact-SQL)](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER (Transact-SQL)](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR (Transact-SQL)](../../t-sql/functions/error-transact-sql.md)  
  
  


