---
title: ERROR_MESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 68439f7a9ea22078660d6e0465961c052002e8be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回导致 TRY…CATCH 构造的 CATCH 块运行的错误的消息文本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>返回值  
 在 CATCH 块中调用时，返回导致 CATCH 块运行的错误消息的完整文本。 该文本包括为所有可替换参数提供的值，如长度、对象名或时间。  
  
 如果在 CATCH 块作用域以外调用，则返回 NULL。  
  
## <a name="remarks"></a>Remarks  
 ERROR_MESSAGE 可以在 CATCH 块作用域内的任意位置调用。  
  
 ERROR_MESSAGE 无论运行多少次，无论在 CATCH 块作用域内的什么位置运行，它都返回错误消息。 这与 @@ERROR 之类的函数形成鲜明对比，后者这样的函数只能在紧接导致错误的语句后面的下一个语句中返回错误号，或者在 CATCH 块的第一个语句中返回错误号。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>C. 在 CATCH 块中将 ERROR_MESSAGE 与其他错误处理工具一起使用  
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
  

