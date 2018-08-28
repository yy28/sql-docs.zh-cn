---
title: '&gt;=（大于或等于）(Transact-SQL)| Microsoft Docs'
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
- Greater
- '>='
- '>= (Greater Than or Equal To)'
- Equal To
- '>=_TSQL'
- Greater Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- greater than or equal to operator (>=)
- '>= (greater than or equal to operator)'
ms.assetid: 641ee28d-7536-46dd-a48a-6c63c2d59278
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0f3c3efd8b6c536076a8e81c75d412ce503a0bf
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082357"
---
# <a name="gt-greater-than-or-equal-to-transact-sql"></a>&gt;=（大于或等于）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比较两个表达式以得出大于或等于的结果（比较运算符）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression >= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 为任意有效的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 两个表达式都必须包含可隐式转换的数据类型。 转换方式取决于[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)的相关规则。  
  
## <a name="result-types"></a>结果类型  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 当比较非空表达式时，如果左边操作数的值大于或等于右边的操作数，则结果为 TRUE；否则结果为 FALSE。  
  
 与 =（等于）比较运算符不同，使用 >= 比较两个 NULL 值的结果不依赖于 ANSI_NULLS 设置。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using--in-a-simple-query"></a>A. 在简单查询中使用 >=  
 下面的示例返回 `HumanResources.Department` 表中其 `DepartmentID` 的值大于或等于 13 的所有行。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID >= 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
13           Quality Assurance  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(4 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [= (Equals) (Transact-SQL)](../../t-sql/language-elements/equals-transact-sql.md)   
 [&#62;（大于）(Transact-SQL)](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
