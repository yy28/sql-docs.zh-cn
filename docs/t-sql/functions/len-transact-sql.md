---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 290d9b9ba27b5895cb9511220bbf7ef39bbb8025
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定字符串表达式的字符数，其中不包含尾随空格。  
  
> [!NOTE]  
>  若要返回用于表示表达式的字节数，请使用 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 函数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>参数  
 string_expression  
 要计算的字符串[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 string_expression 可以是常量、变量，也可以是字符列或二进制数据列。  
  
## <a name="return-types"></a>返回类型  
 bigint（如果 expression 的数据类型为 varchar(max)、nvarchar (max) 或 varbinary(max)）；否则为 int。  
  
 如果使用 SC 排序规则，则返回的整数值将 UTF-16 代理项对作为单个字符计数。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="remarks"></a>Remarks  
 LEN 不包括尾随空格。 如果这是个问题，请考虑使用 [DATALENGTH (Transact-SQL)](../../t-sql/functions/datalength-transact-sql.md) 函数，该函数不会修整字符串。 如果处理的是 unicode 字符串，DATALENGTH 将返回两倍的字符数。 以下示例演示 LEN 和带有尾随空格的 DATALENGTH。  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>示例  
 以下示例在 `FirstName` 地区的人的 `Australia` 中选择字符数和数据。 本示例使用 AdventureWorks 数据库。  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例返回 `FirstName` 列中的字符数，以及位于 `Australia` 中的员工的姓氏和名字。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>另请参阅  
 [DATALENGTH (Transact-SQL)](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX (Transact-SQL)](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX (Transact-SQL)](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT (Transact-SQL)](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT (Transact-SQL)](../../t-sql/functions/right-transact-sql.md)  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
  
  


