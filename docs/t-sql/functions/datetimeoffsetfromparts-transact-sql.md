---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 09e705fd426963018eadae7351df1046d3d1ef0c
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698268"
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

此函数返回指定日期和时间参数的 datetimeoffset 值。 返回值包含精度参数指定的精度，小时和分钟偏移参数确定的偏移量。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>参数  
year  
指定年份的整数表达式。
  
month  
指定月份的整数表达式。
  
day  
指定日期的整数表达式。
  
hour  
指定小时的整数表达式。
  
minute  
指定分钟的整数表达式。
  
*seconds*  
指定秒数的整数表达式。
  
fractions  
指定小数值的整数表达式。
  
hour_offset  
整数表达式，用于指定时区偏移量的小时部分。
  
minute_offset  
整数表达式，用于指定时区偏移量的分钟部分。
  
*精度*  
整数文本，用于指定 `DATETIMEOFFSETFROMPARTS` 要返回的 datetimeoffset 值的精度。
  
## <a name="return-types"></a>返回类型
**datetimeoffset(** precision **)**
  
## <a name="remarks"></a>Remarks  
`DATETIMEOFFSETFROMPARTS` 返回已完全初始化的 datetimeoffset 数据类型。 `DATETIMEOFFSETFROMPARTS` 使用偏移参数来表示时区偏移量。 如果省略偏移参数，`DATETIMEOFFSETFROMPARTS` 假定时区偏移量为 00:00，换言之，即根本没有时区偏移量。 对于指定的偏移参数，`DATETIMEOFFSETFROMPARTS` 需要这两个参数的值，这些参数要么都是正值，要么都是负值。 对于没有指定 hour_offset 值的指定 minute_offset，`DATETIMEOFFSETFROMPARTS` 将引发错误。 如果其他参数具有无效值，`DATETIMEOFFSETFROMPARTS` 将引发错误。 如果至少有一个必需参数具有 NULL 值，则 `DATETIMEOFFSETFROMPARTS` 返回 NULL。 但是，如果 precision 参数具有 NULL 值，`DATETIMEOFFSETFROMPARTS` 将引发错误。
  
fractions 参数取决于 precision 参数。 例如，如果 precision 值为 7，则每个分数表示 100 纳秒；如果 precision 为 3，则每个分数表示 1 毫秒。 如果 precision 的值为零，则 fractions 的值也必须为零；否则 `DATETIMEOFFSETFROMPARTS` 将引发错误。

此函数支持在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 及更高版本的服务器上远程执行。 但不支持在版本低于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的服务器上远程执行。
  
## <a name="examples"></a>示例  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. 不包含秒的小数部分的示例  
  
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
此示例演示了 fractions 和 precision 参数的用法：
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
  
  


