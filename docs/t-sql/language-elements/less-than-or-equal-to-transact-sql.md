---
title: '&lt;=（小于或等于）(Transact-SQL)| Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- <=
- Less
- Equal To
- <=_TSQL
- Less Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 1f05474c-0377-48cb-b567-9d85d0c40479
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 69703b0793a8282005e5411786d51bc2d8282131
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36248589"
---
# <a name="lt-less-than-or-equal-to-transact-sql"></a>&lt;=（小于或等于）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比较两个表达式（比较运算符）。 比较非空表达式时，如果左边操作数的值小于或等于右边的操作数，则结果为 TRUE；否则结果为 FALSE。  
  
 与 =（等于）比较运算符不同，使用 >= 比较两个 NULL 值的结果不依赖于 ANSI_NULLS 设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression <= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 为任意有效的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 两个表达式都必须包含可隐式转换的数据类型。 转换方式取决于[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)的相关规则。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="examples"></a>示例  
  
### <a name="a-using--in-a-simple-query"></a>A. 在简单查询中使用 <=  
 下面的示例返回 `HumanResources.Department` 表中其 `DepartmentID` 的值小于或等于 3 的所有行。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID <= 3  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
1            Engineering  
2            Tool Design  
3            Sales  
  
(3 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
