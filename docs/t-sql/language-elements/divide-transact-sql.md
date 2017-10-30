---
title: "（除）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /
- /_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- / (divide)
- division [SQL Server]
- divide operator (/)
ms.assetid: 1d69893b-e5c3-441d-8dd8-0e5eb872ecfc
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e3e8a94a92ca592ce6a2deb5d13915606f04f984
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="divide-transact-sql"></a>（除）(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  用一个数除以另一个数（算术除法运算符）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
dividend / divisor  
```  
  
## <a name="arguments"></a>参数  
 *被除数*  
 被除数的数值表达式。 *被除数*可以是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)任何一种数值数据类型的数据类型类别中，除**datetime**和**smalldatetime**数据类型。  
  
 *除数*  
 是用于除以被除数的数值表达式。 *除数*可以是除之外的任何一种数值数据类型类别的数据类型的任何有效表达式**datetime**和**smalldatetime**数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
 如果整数*被除数*除以整数*除数*，结果是一个整数，已截断的任何的结果小数部分。  
  
## <a name="remarks"></a>注释  
 / 运算符返回的实际值是用第一个表达式除以第二个表达式所得的商。  
  
## <a name="examples"></a>示例  
 以下示例将使用除法算术运算符来计算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 中销售人员的每月销售目标。  
  
```  
-- Uses AdventureWorks  
  
SELECT s.BusinessEntityID AS SalesPersonID, FirstName, LastName, SalesQuota, SalesQuota/12 AS 'Sales Target Per Month'  
FROM Sales.SalesPerson AS s   
JOIN HumanResources.Employee AS e   
    ON s.BusinessEntityID = e.BusinessEntityID  
JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 以下为部分结果集。  
  
```  
  
SalesPersonID FirstName    LastName          SalesQuota  Sales Target Per Month  
------------- ------------ ----------------- ----------- ------------------  
274           Stephen      Jiang             NULL        NULL  
275           Michael      Blythe            300000.00   25000.00  
276           Linda        Mitchell          250000.00   20833.3333  
277           Jillian      Carson            250000.00   20833.3333  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例使用除法算术运算符来计算简单到名病小时的每个员工的休假小时数的比率。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, VacationHours/SickLeaveHours AS PersonalTimeRatio  
FROM DimEmployee;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [&#40; 划分等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



