---
title: "COT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COT_TSQL
- COT
dev_langs:
- TSQL
helpviewer_keywords:
- COT function
- cotangent
ms.assetid: c87a9dac-e398-4125-80c3-7df3c2ce6b63
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d799d83336507aba7b582796f730c53d7ae4840e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cot-transact-sql"></a>COT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

数学函数的返回以弧度表示，在指定的指定角度的三角余切**float**表达式。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
COT ( float_expression )  
```  
  
## <a name="arguments"></a>参数  
*float_expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)类型的**float**或可以隐式转换为的类型**float**。
  
## <a name="return-types"></a>返回类型
**float**
  
## <a name="examples"></a>示例  
以下示例返回指定角度的 COT 值。
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
以下示例返回指定角度的 COT 值。
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


