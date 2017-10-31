---
title: "DATETIMEOFFSETFROMPARTS (Transact SQL) |Microsoft 文档"
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 665607c3b6ea9411d90137fba416d96d3d46a4c1
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回**datetimeoffset**值的指定的日期和时间并使用指定的偏移量和精度。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
  
*分钟*  
用于指定分钟的整数表达式。
  
*seconds*  
用于指定秒的整数表达式。
  
*分数 （竖式)*  
用于指定小数部分的整数表达式。
  
*hour_offset*  
整数表达式，用于指定时区偏移量的小时部分。
  
*minute_offset*  
整数表达式，用于指定时区偏移量的分钟部分。
  
*精度*  
指定的精度的整数文本**datetimeoffset**要返回值。
  
## <a name="return-types"></a>返回类型
**datetimeoffset (** *精度* **)**
  
## <a name="remarks"></a>注释  
**DATETIMEOFFSETFROMPARTS**返回完全初始化**datetimeoffset**数据类型。 偏移量参数用来表示时区偏移量。 如果忽略偏移量参数，则认为时区偏移量是 00:00，也即没有时区偏移量。 如果指定了偏移量参数，则必须存在这两个参数，且两者必须为正数或负数。 如果*minute_offset*指定了不含*hour_offset*，将引发错误。 如果其他参数无效，则引发错误。 如果需要自变量为 null，则返回 null。 但是，如果*精度*自变量为 null，则引发错误。
  
*分数 （竖式)*取决于自变量*精度*自变量。 例如，如果*精度*为 7，则每个部分表示 100 纳秒; 如果*精度*为 3，则每个部分表示以毫秒为单位。 如果值*精度*为零，则值*分数 （竖式)*还必须为零; 否则，将引发错误。
  
此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 它将不到具有以下版本的服务器进行远程处理[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小数部分的简单示例  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 包含秒的小数部分的示例  
下面的示例演示了利用*分数 （竖式)*和*精度*参数：
1.   当*分数 （竖式)*的值为 5 和*精度*具有值为 1，然后将值*分数 （竖式)*表示 5/10 的第二个。  
1.   当*分数 （竖式)*的值为 50 和*精度*具有值为 2，然后将值*分数 （竖式)*表示的第二个 50/100。  
1.   当*分数 （竖式)*的值为 500 和*精度*具有值 3，然后将值*分数 （竖式)*表示 500/1000 的第二个。  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[时区 &AMP;#40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  



