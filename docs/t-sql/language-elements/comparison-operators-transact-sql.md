---
title: "比较运算符 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 45c0e85b89d542dce815104eb8e831169599227b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="comparison-operators-transact-sql"></a>比较运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  比较运算符测试两个表达式是否相同。 可以对除外的表达式的所有表达式使用比较运算符**文本**， **ntext**，或**映像**数据类型。 下表列出了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 比较运算符。  
  
|运算符|含义|  
|--------------|-------------|  
|[=（等于）](../../t-sql/language-elements/equals-transact-sql.md)|等于|  
|[>（大于）](../../t-sql/language-elements/greater-than-transact-sql.md)|大于|  
|[<（小于）](../../t-sql/language-elements/less-than-transact-sql.md)|小于|  
|[>=（大于或等于）](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|大于或等于|  
|[<=（小于或等于）](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|小于或等于|  
|[<>（不等于）](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|不等于|  
|[!=（不等于）](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|不等于（非 ISO 标准）|  
|[!<（不小于）](../../t-sql/language-elements/not-less-than-transact-sql.md)|不小于（非 ISO 标准）|  
|[!>（不大于）](../../t-sql/language-elements/not-greater-than-transact-sql.md)|不大于（非 ISO 标准）|  
  
## <a name="boolean-data-type"></a>Boolean 数据类型  
 比较运算符的结果具有**布尔**数据类型。 它有三个值：TRUE、FALSE 和 UNKNOWN。 返回的表达式**布尔**数据类型被称为布尔表达式。  
  
 与其他不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，**布尔**数据类型不能指定为变量或表列的数据类型，因而无法在结果集中返回。  
  
 当 SET ANSI_NULLS 为 ON 时，带有一个或两个 NULL 表达式的运算符返回 UNKNOWN。 当 SET ANSI_NULLS 为 OFF 时，上述规则同样适用，但是两个表达式均为 NULL，则等号 (=) 运算符返回 TRUE。 例如，如果 SET ANSI_NULLS 为 OFF，则 NULL = NULL 返回 TRUE。  
  
 使用表达式**布尔**限定的搜索条件并在控制流语言语句如作为 IF 和时，例如的行进行过滤的 WHERE 子句中使用数据类型：  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>另请参阅  
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
