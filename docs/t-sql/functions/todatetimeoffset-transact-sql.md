---
title: "TODATETIMEOFFSET (Transact SQL) |Microsoft 文档"
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
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6c0ff45ae5842950d9f15d7b131ad107fba351b5
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回**datetimeoffset**从转换的值**datetime2**表达式。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)解析为[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)值。  
  
> [!NOTE]  
>  表达式的类型不能为**文本**， **ntext**，或**映像**因为这些类型不能隐式转换为**varchar**或**nvarchar**。  
  
 *time_zone*  
 是表示时区偏移量（分钟）（如果为整数）的表达式，例如 -120；或表示小时和分钟数的表达式（如果为字符串），例如“+13.00”。 范围为 +14 到 -14（小时）。 该表达式被解释为指定 time_zone 的本地时间。  
  
> [!NOTE]  
>  如果表达式是字符串，其格式必须为 {+|-}TZH:THM。  
  
## <a name="return-type"></a>返回类型  
 **datetimeoffset**。 小数精度等同于*datetime*自变量。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 更改当前日期和时间的时区偏移量  
 下面的示例将当前日期和时间的时区偏移量更改为时区 `-07:00`。  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. 更改时区偏移量（以分钟为单位）  
 下面的示例将当前时区更改为 `-120` 分钟。  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 添加 13 小时时区偏移量  
 下面的示例将 13 小时时区偏移量添加到日期和时间。  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [时区 &AMP;#40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


