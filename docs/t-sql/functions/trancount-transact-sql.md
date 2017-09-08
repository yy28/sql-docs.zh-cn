---
title: "@@TRANCOUNT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19713aeb9058e83f97500075a1024c6c715628e9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40trancount-transact-sql"></a>& #x 40; 和 #x 40;Trancount (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回在当前连接上执行的 BEGIN TRANSACTION 语句的数目。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 BEGIN TRANSACTION 语句递增@TRANCOUNT1。 @ ROLLBACK TRANSACTION 递减@TRANCOUNT为 0，除外 ROLLBACK TRANSACTION *savepoint_name*，这不影响@TRANCOUNT。 COMMIT TRANSACTION 或递减提交工作@TRANCOUNT1。  
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>A. 演示 BEGIN 和 COMMIT 语句的效果  
 下面的示例演示嵌套的 `BEGIN` 和 `COMMIT` 语句对 `@@TRANCOUNT` 变量产生的效果。  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>B. 演示 BEGIN 和 ROLLBACK 语句的效果  
 下面的示例演示嵌套的 `BEGIN TRAN` 和 `ROLLBACK` 语句对 `@@TRANCOUNT` 变量产生的效果。  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

