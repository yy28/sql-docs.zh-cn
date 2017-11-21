---
title: "@@ROWCOUNT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411dc7eb628ddff52eb2f9426488e05860c9d279
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40rowcount-transact-sql"></a>& #x 40; 和 #x 40;行计数 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回受上一语句影响的行数。 如果多个 20 亿行数，则使用[ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]语句可以设置中的值 @@ROWCOUNT通过以下方式：  
  
-   设置@ROWCOUNT到的行数受影响或读取。 可以将行发送到客户端，也可以不发送。  
  
-   保留@ROWCOUNT从上一次的语句执行。  
  
-   重置@ROWCOUNT为 0，但不是返回到客户端的值。  
  
 请始终设置简单赋值的语句 @@ROWCOUNT值设置为 1。 不将任何行发送到客户端。 这些语句的示例包括： 设置*local_variable*，则返回，READTEXT，然后选择而无需查询语句，例如选择 getdate （） 函数或选择*通用文本***'**.  
  
 在查询中进行赋值或在查询集中使用返回的语句 @@ROWCOUNT到的行数的值影响，或者读取查询，例如： 选择*local_variable* = c1 FROM t1。  
  
 数据操作语言 (DML) 语句将设置 @@ROWCOUNT值的查询受影响的行数和该值返回到客户端。 DML 语句不会将任何行发送到客户端。  
  
 DECLARE CURSOR 和设置的提取 @@ROWCOUNT值设置为 1。  
  
 EXECUTE 语句保留以前的 @@ROWCOUNT。  
  
 语句使用，如设置\<选项 >、 释放 CURSOR、 关闭游标、 BEGIN TRANSACTION 或 COMMIT TRANSACTION 行计数值重置为 0。  
  
 本机编译存储的过程保留以前的 @@ROWCOUNT。 [!INCLUDE[tsql](../../includes/tsql-md.md)]本机编译存储过程中的语句不设置@ROWCOUNT。 有关详细信息，请参阅[Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
## <a name="examples"></a>示例  
 以下示例执行 `UPDATE` 语句并使用 `@@ROWCOUNT` 来检测是否更改了任何行。  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [设置行计数 &#40;Transact SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

