---
title: '%（取模）(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- modulo
- modulus
- '% (Modulo)'
- '% (Modulus)'
- MOD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '% (modulo operator)'
- '% (modulus operator)'
- remainder of division operation
- modulo operator (%)
- modulus operator (%)
ms.assetid: f93c662e-f405-486e-bf23-a2d03907b5bd
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: c970fee639c007ab2acf237015abf700a213f8b8
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453332"
---
# <a name="-modulus-transact-sql"></a>%（取模）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回两数相除后的余数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
dividend % divisor  
```  
  
## <a name="arguments"></a>参数  
 *被除数*  
 被除数的数值表达式。 *dividend* 必须为整数和货币数据类型类别中任意一种数据类型的有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，或者为 **numeric** 数据类型。  
  
 *除数*  
 除数的数值表达式。 divisor 必须为整数和货币数据类型类别中任意一种数据类型的任意有效表达式，或者为 numeric 数据类型。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。  
  
## <a name="remarks"></a>Remarks  
 取模算术运算符可以和列名、数值常量或任何具有整数和货币数据类型类别或 numeric 数据类型的有效表达式组合一起用于 SELECT 语句的选择列表中。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example"></a>A. 简单示例  
 下面的示例用 38 除以数字 5。 所得结果的整数部分为 7。该示例演示了取模运算如何返回余数 3。  
  
```  
SELECT 38 / 5 AS Integer, 38 % 5 AS Remainder ;  
  
```  
  
### <a name="b-example-using-columns-in-a-table"></a>B. 使用表中的列的示例  
 以下示例返回产品 ID 号、产品单价、除以每种产品的单价后得到的模（余数）、转换为整数值，以及订购的产品数。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(100)ProductID, UnitPrice, OrderQty,  
   CAST((UnitPrice) AS int) % OrderQty AS Modulo  
FROM Sales.SalesOrderDetail;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example"></a>C：简单示例  
 以下示例显示将 3 除以 2 时运算符 `%` 的结果。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) 3%2 FROM dimEmployee;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
1         
```  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [LIKE (Transact-SQL)](../../t-sql/language-elements/like-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [%=（取模赋值）(Transact-SQL)](../../t-sql/language-elements/modulo-equals-transact-sql.md)   
 [复合运算符 (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


