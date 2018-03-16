---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c8a5f8bea3bf6ca97e0f7b4a35f8f78315716df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

对指定的日期和时间返回 datetimeoffset 值，即具有指定的偏移量和精度。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>参数  
year  
用于指定年度的整数表达式。
  
month  
用于指定月份的整数表达式。
  
day  
用于指定日期的整数表达式。
  
hour  
用于指定小时的整数表达式。
  
minute  
用于指定分钟的整数表达式。
  
*seconds*  
用于指定秒的整数表达式。
  
fractions  
用于指定小数部分的整数表达式。
  
hour_offset  
整数表达式，用于指定时区偏移量的小时部分。
  
minute_offset  
整数表达式，用于指定时区偏移量的分钟部分。
  
*精度*  
整数文字，用于指定要返回的 datetimeoffset 值的精度。
  
## <a name="return-types"></a>返回类型
**datetimeoffset(** precision **)**
  
## <a name="remarks"></a>Remarks  
DATETIMEOFFSETFROMPARTS 返回完全初始化的 datetimeoffset 数据类型。 偏移量参数用来表示时区偏移量。 如果忽略偏移量参数，则认为时区偏移量是 00:00，也即没有时区偏移量。 如果指定了偏移量参数，则必须存在这两个参数，且两者必须为正数或负数。 如果指定了 minute_offset，但没有 hour_offset，则会引发错误。 如果其他参数无效，则引发错误。 如果所需的参数为 null，则返回 null。 但是，如果 precision 参数为 Null，则会引发错误。
  
fractions 参数取决于 precision 参数。 例如，如果 precision 为 7，则每个分数表示 100 纳秒；如果 precision 为 3，则每个分数表示 1 毫秒。 如果 precision 的值为零，则 fractions 的值也必须为零；否则将引发错误。
  
此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 但在低于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的服务器版本中无法远程执行。
  
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
以下示例演示了 fractions 和 precision 参数的用法：
1.   如果 fractions 的值为 5、precision 的值为 1，则 fractions 的值表示 5/10 秒。  
1.   如果 fractions 的值为 50、precision 的值为 2，则 fractions 的值表示 50/100 秒。  
1.   如果 fractions 的值为 500、precision 的值为 3，则 fractions 的值表示 500/1000 秒。  
  
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
[AT TIME ZONE (Transact-SQL)](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


