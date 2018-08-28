---
title: SET XACT_ABORT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- XACT_ABORT_TSQL
- XACT_ABORT
- SET XACT_ABORT
- SET_XACT_ABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- XACT_ABORT option
- automatic transaction roll backs
- transactions [SQL Server], rolling back
- rolling back transactions, SET XACT_ABORT
- roll back transactions [SQL Server]
- SET XACT_ABORT statement
ms.assetid: cbcaa433-58f2-4dc3-a077-27273bef65b5
caps.latest.revision: 50
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4c34589ccb52e9cdc9a21ae66bb1b9f4bff2a7e4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43083805"
---
# <a name="set-xactabort-transact-sql"></a>SET XACT_ABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

    
> [!NOTE]  
>  THROW 语句执行 SET XACT_ABORT。 RAISERROR 则不执行。 新应用程序应使用 THROW 而不是 RAISERROR。  
  
 指定当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句出现运行时错误时，[!INCLUDE[tsql](../../includes/tsql-md.md)] 是否自动回滚当前事务。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```    
SET XACT_ABORT { ON | OFF }  
```  

  
## <a name="remarks"></a>Remarks  
 当 SET XACT_ABORT 为 ON 时，如果执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句产生运行时错误，则整个事务将终止并回滚。  
  
 当 SET XACT_ABORT 为 OFF 时，有时只回滚产生错误的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，而事务将继续进行处理。 如果错误很严重，那么即使 SET XACT_ABORT 为 OFF，也可能回滚整个事务。 OFF 是默认设置。  
  
 编译错误（如语法错误）不受 SET XACT_ABORT 的影响。  
  
 对于大多数 OLE DB 访问接口（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]），必须将隐式或显示事务中的数据修改语句中的 XACT_ABORT 设置为 ON。 唯一不需要该选项的情况是在提供程序支持嵌套事务时。  
  
 当 ANSI_WARNINGS=OFF 时，违反权限的行为导致事务中止。  
  
 SET XACT_ABORT 的设置是在执行或运行时设置，而不是在分析时设置。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @XACT_ABORT VARCHAR(3) = 'OFF';  
IF ( (16384 & @@OPTIONS) = 16384 ) SET @XACT_ABORT = 'ON';  
SELECT @XACT_ABORT AS XACT_ABORT;  
  
```  
  
## <a name="examples"></a>示例  
 下列代码示例导致在含有其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的事务中发生外键冲突错误。 在第一个语句集中产生错误，但其他语句均成功执行且事务成功提交。 在第二个语句集中，将 `SET XACT_ABORT` 设置为 `ON`。 这导致语句错误使批处理终止，并使事务回滚。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't2', N'U') IS NOT NULL  
    DROP TABLE t2;  
GO  
IF OBJECT_ID(N't1', N'U') IS NOT NULL  
    DROP TABLE t1;  
GO  
CREATE TABLE t1  
    (a INT NOT NULL PRIMARY KEY);  
CREATE TABLE t2  
    (a INT NOT NULL REFERENCES t1(a));  
GO  
INSERT INTO t1 VALUES (1);  
INSERT INTO t1 VALUES (3);  
INSERT INTO t1 VALUES (4);  
INSERT INTO t1 VALUES (6);  
GO  
SET XACT_ABORT OFF;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (1);  
INSERT INTO t2 VALUES (2); -- Foreign key error.  
INSERT INTO t2 VALUES (3);  
COMMIT TRANSACTION;  
GO  
SET XACT_ABORT ON;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (4);  
INSERT INTO t2 VALUES (5); -- Foreign key error.  
INSERT INTO t2 VALUES (6);  
COMMIT TRANSACTION;  
GO  
-- SELECT shows only keys 1 and 3 added.   
-- Key 2 insert failed and was rolled back, but  
-- XACT_ABORT was OFF and rest of transaction  
-- succeeded.  
-- Key 5 insert error with XACT_ABORT ON caused  
-- all of the second transaction to roll back.  
SELECT *  
    FROM t2;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [THROW (Transact-SQL)](../../t-sql/language-elements/throw-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  
