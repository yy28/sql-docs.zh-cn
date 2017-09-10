---
title: "DATEFROMPARTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3365c40b5bc4fb57a8e09cc97e706a16fbd709ec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回**日期**指定的年、 月和日的值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>参数  
*年*  
用于指定年度的整数表达式。
  
*月*  
指定月份（从 1 到 12）的整数表达式。
  
*一天*  
用于指定日期的整数表达式。
  
## <a name="return-types"></a>返回类型
**date**
  
## <a name="remarks"></a>注释  
**DATEFROMPARTS**返回**日期**值，该值设置为指定的年、 月和日的日期部分，设置为默认的时间部分。 如果自变量无效，则引发错误。 如果所需的参数为 null，则返回 null。
  
此函数可以在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 服务器以及更高版本上远程执行。 但在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 之下的服务器版本中无法远程执行。
  
## <a name="examples"></a>示例  
下面的示例演示**DATEFROMPARTS**函数。
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下面的示例演示**DATEFROMPARTS**函数。
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)
  
  


