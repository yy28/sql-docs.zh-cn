---
title: "复制 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLICATE_TSQL
- REPLICATE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], repeating
- REPLICATE function
- repeating character expressions
ms.assetid: 0cd467fb-3f22-471a-892c-0039d9f7fa1a
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2260073409ce6d7b558c65f2528f63423fdf1eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="replicate-transact-sql"></a>REPLICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  以指定的次数重复字符串值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
REPLICATE ( string_expression ,integer_expression )   
```  
  
## <a name="arguments"></a>参数  
 *string_expression*  
 字符串或二进制数据类型的表达式。 *string_expression*可以是字符或二进制数据。  
  
> [!NOTE]  
>  如果*string_expression*的类型不是**varchar （max)**或**nvarchar (max)**，复制将截断为 8000 个字节的返回值。 返回值大于 8000 个字节， *string_expression*必须显式转换为相应的大型值数据类型。  
  
 *integer_expression*  
 是一个表达式的任何整数类型，包括**bigint**。 如果*integer_expression*为负，则返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 返回与相同的类型*string_expression*。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-replicate"></a>A. 使用 REPLICATE  
 以下示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中生产行代码的前面将 `0` 字符复制四次。  
  
```  
SELECT [Name]  
, REPLICATE('0', 4) + [ProductLine] AS 'Line Code'  
FROM [Production].[Product]  
WHERE [ProductLine] = 'T'  
ORDER BY [Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                                               Line Code  
-------------------------------------------------- ---------  
HL Touring Frame - Blue, 46                        0000T   
HL Touring Frame - Blue, 50                        0000T   
HL Touring Frame - Blue, 54                        0000T   
HL Touring Frame - Blue, 60                        0000T   
HL Touring Frame - Yellow, 46                      0000T   
HL Touring Frame - Yellow, 50                      0000T  
...  
```  
  
### <a name="b-using-replicate-and-datalength"></a>B. 使用 REPLICATE 和 DATALENGTH  
 以下示例中，数值从数值数据类型转换为字符型或 Unicode 型时，从左填充数字使达到指定的长度。  
  
```  
IF EXISTS(SELECT name FROM sys.tables  
      WHERE name = 't1')  
   DROP TABLE t1;  
GO  
CREATE TABLE t1   
(  
 c1 varchar(3),  
 c2 char(3)  
);  
GO  
INSERT INTO t1 VALUES ('2', '2'), ('37', '37'),('597', '597');  
GO  
SELECT REPLICATE('0', 3 - DATALENGTH(c1)) + c1 AS 'Varchar Column',  
       REPLICATE('0', 3 - DATALENGTH(c2)) + c2 AS 'Char Column'  
FROM t1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Varchar Column        Char Column  
--------------------  ------------  
002                   2    
037                   37   
597                   597  
  
(3 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-replicate"></a>C： 使用复制  
 下面的示例将复制`0`四次前端中的字符`ItemCode`值。  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName AS Name,  
   ProductAlternateKey AS ItemCode,  
   REPLICATE('0', 4) + ProductAlternateKey AS FullItemCode  
FROM dbo.DimProduct  
ORDER BY Name;  
```  
  
 以下是在结果集中的前几行。  
  
 `Name                     ItemCode       FullItemCode`  
  
 `------------------------ -------------- ---------------`  
  
 `Adjustable Race          AR-5381        0000AR-5381`  
  
 `All-Purpose Bike Stand   ST-1401        0000ST-1401`  
  
 `AWC Logo Cap             CA-1098        0000CA-1098`  
  
 `AWC Logo Cap             CA-1098        0000CA-1098`  
  
 `AWC Logo Cap             CA-1098        0000CA-1098`  
  
 `BB Ball Bearing          BE-2349        0000BE-2349`  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


