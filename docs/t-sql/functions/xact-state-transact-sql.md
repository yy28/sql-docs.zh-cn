---
title: XACT_STATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f8b63625f4e0af0e1f6c55b2d85ae8bb10d53b02
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="xactstate-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  用于报告当前正在运行的请求的用户事务状态的标量函数。 XACT_STATE 指示请求是否有活动的用户事务，以及是否能够提交该事务。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
XACT_STATE()  
```  
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 XACT_STATE 返回下列值。  
  
|返回值|含义|  
|------------------|-------------|  
|@shouldalert|当前请求有活动的用户事务。 请求可以执行任何操作，包括写入数据和提交事务。|  
|0|当前请求没有活动的用户事务。|  
|-1|当前请求具有活动的用户事务，但出现了致使事务被归类为无法提交的事务的错误。 请求无法提交事务或回滚到保存点；它只能请求完全回滚事务。 请求在回滚事务之前无法执行任何写操作。 请求在回滚事务之前只能执行读操作。 事务回滚之后，请求便可执行读写操作并可开始新的事务。<br /><br /> 当最外面的批处理运行完时，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 会自动回滚所有不可提交的活跃事务。 如果事务进入不可提交状态时未发送错误消息，则当批处理结束时，将向客户端应用程序发送一个错误消息。 此消息指示检测到并回滚了一个不可提交的事务。|  
  
 XACT_STATE 和 @@TRANCOUNT 函数都可用于检测当前请求是否具有活动的用户事务。 @@TRANCOUNT 不能用于确定事务是否已分类为不可提交的事务。 XACT_STATE 不能用于确定是否有嵌套事务。  
  
## <a name="examples"></a>示例  
 下面的示例使用`XACT_STATE` 构造的 `CATCH` 块中的 `TRY…CATCH` 来确定是提交事务还是回滚事务。 由于 `SET XACT_ABORT` 设置为 `ON`，因此违反约束的错误将导致事务进入无法提交的状态。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
