---
title: "DATETIME2FROMPARTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce109671228e82bc0f02e9920b2ef98c9bbcdb83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回**datetime2**值的指定的日期和时间并使用指定的精度。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>参数  
*年*  
用于指定年度的整数表达式。
  
*月*  
用于指定月份的整数表达式。
  
*一天*  
用于指定日期的整数表达式。
  
 *小时*  
用于指定小时的整数表达式。
  
*分钟*整数表达式，指定分钟。
  
*seconds*  
用于指定秒的整数表达式。
  
*分数 （竖式)*  
用于指定小数部分的整数表达式。
  
*精度*  
指定的精度的整数文本**datetime2**要返回值。
  
## <a name="return-types"></a>返回类型
**datetime2 (** *精度* **)**
  
## <a name="remarks"></a>注释  
**DATETIME2FROMPARTS**返回完全初始化**datetime2**值。 如果自变量不是有效的将引发错误。 如果所需的参数为 null，则返回 null。 但是，如果*精度*自变量为 null，则引发错误。
  
*分数 （竖式)*取决于自变量*精度*自变量。 例如，如果*精度*为 7，则每个部分表示 100 纳秒; 如果*精度*为 3，则每个部分表示以毫秒为单位。 如果值*精度*为零，则值*分数 （竖式)*还必须为零; 否则，将引发错误。
  
此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 它将不到具有以下版本的服务器进行远程处理[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小数部分的简单示例  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 包含秒的小数部分的示例  
下面的示例演示了利用*分数 （竖式)*和*精度*参数：
  
1.  当*分数 （竖式)*的值为 5 和*精度*具有值为 1，然后将值*分数 （竖式)*表示 5/10 的第二个。  
  
2.  当*分数 （竖式)*的值为 50 和*精度*具有值为 2，然后将值*分数 （竖式)*表示的第二个 50/100。  
  
3.  当*分数 （竖式)*的值为 500 和*精度*具有值 3，然后将值*分数 （竖式)*表示 500/1000 的第二个。  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[datetime2 (Transact-SQL)](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

