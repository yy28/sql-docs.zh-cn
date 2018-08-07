---
title: ERROR_MESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 839432fa621b81c16627140164549772996cc68d
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452801"
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数返回错误的消息文本，该错误导致执行了 TRY…CATCH 构造的 CATCH 块。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>返回值  
在 CATCH 块中调用时，`ERROR_MESSAGE` 返回导致 `CATCH` 块运行的错误消息的完整文本。 该文本包括为所有可替换参数提供的值，例如长度、对象名或时间。  
  
在 CATCH 块作用域外调用时，`ERROR_MESSAGE` 返回 NULL。  
  
## <a name="remarks"></a>Remarks  
`ERROR_MESSAGE` 支持在 CATCH 块作用域内的任意位置调用。  
  
无论 `ERROR_MESSAGE` 运行多少次或在 `CATCH` 块作用域内的任意位置运行，它都将返回相关的错误消息。 这与 @@ERROR 之类的函数不同，后者只在导致错误的语句的后一个语句中返回错误号。  
  
在嵌套 `CATCH` 块中，`ERROR_MESSAGE` 返回特定于引用该 `CATCH` 块的 `CATCH` 块的作用域的错误消息。 例如，外部 TRY...CATCH 构造的 `CATCH` 块可能具有内部 `TRY...CATCH` 构造。 在该内部 `CATCH` 块内，`ERROR_MESSAGE` 将返回调用内部 `CATCH` 块的错误消息。 如果 `ERROR_MESSAGE` 在外部 `CATCH` 块中运行，它将返回调用该外部 `CATCH` 块的错误消息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. 在 CATCH 块中使用 ERROR_MESSAGE  
此示例显示生成被零除错误的 `SELECT` 语句。 `CATCH` 块返回错误消息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorMessage
----------------------------------
Divide by zero error encountered.

(1 row(s) affected)

```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. 在 CATCH 块中将 ERROR_MESSAGE 与其他错误处理工具一起使用  
此示例显示生成被零除错误的 `SELECT` 语句。 `CATCH` 块将返回错误消息和有关此错误的信息。  
  
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

-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine  ErrorMessage
----------- ------------- ----------- --------------- ---------- ----------------------------------
8134        16            1           NULL            4          Divide by zero error encountered.

(1 row(s) affected)

```
  

