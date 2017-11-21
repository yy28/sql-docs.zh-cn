---
title: "ISDATE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- ISDATETIME
- ISDATE_TSQL
- ISDATE
- ISDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], ISDATE
- validate dates times [SQL Server]
- formats [SQL Server], time
- dates [SQL Server], validate
- verify dates times [SQL Server]
- functions [SQL Server], time
- formats [SQL Server], dates
- functions [SQL Server], date and time
- time [SQL Server], functions
- time [SQL Server], validate
- ISDATE function [SQL Server]
ms.assetid: 8e2c9ee7-388a-432f-b2c9-7b398f26bf85
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e005b11ad15170dcc2f6f45441d62e6ccc29570
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="isdate-transact-sql"></a>ISDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  如果返回 1*表达式*是一个有效**日期**，**时间**，或**datetime**值; 否则为 0。  
  
 如果将 ISDATE 返回 0*表达式*是**datetime2**值。  
  
 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md). 请注意，datetime 数据的范围为 1753-01-01 至 9999-12-31，而日期数据的范围为 0001-01-01 至 9999-12-31。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ISDATE ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是一个字符串或[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，可以转换为字符字符串。 表达式的长度不得超过 4,000 个字符。 不允许将日期和时间数据类型（datetime 和 smalldatetime 除外）作为 ISDATE 的参数。  
  
## <a name="return-type"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 ISDATE 是仅当你将其用于确定[转换](../../t-sql/functions/cast-and-convert-transact-sql.md)函数，如果指定 CONVERT 样式参数，并且样式不等于 0、 100、 9 或 109。  
  
 ISDATE 的返回值取决于设置的设置[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)， [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[配置默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)。  
  
## <a name="isdate-expression-formats"></a>ISDATE 表达式格式  
 有关 ISDATE 将为其返回 1，有效格式的示例中，请参阅"支持字符串格式的日期时间"的部分[datetime](../../t-sql/data-types/datetime-transact-sql.md)和[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)主题。 有关其他示例，另请参阅的"自变量"部分的输入/输出列[CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
 下表概述了无效的输入表达式格式（返回 0 或错误）。  
  
|ISDATE 表达式|ISDATE 返回值|  
|-----------------------|-------------------------|  
|NULL|0|  
|中列出的数据类型值[数据类型](../../t-sql/data-types/data-types-transact-sql.md)字符串、 Unicode 字符字符串，或日期和时间以外的任何数据类型类别中。|0|  
|值的**文本**， **ntext**，或**映像**数据类型。|0|  
|秒精度小数位数超过 3 的任何值（.0000 到 .0000000...n）。 ISDATE 将返回 0，如果*表达式*是**datetime2**值，但如果将返回 1*表达式*是一个有效**datetime**值。|0|  
|有效日期和无效值混在一起的任何值，例如 1995-10-1a。|0|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-isdate-to-test-for-a-valid-datetime-expression"></a>A. 使用 ISDATE 测试是否为有效的 datetime 表达式  
 下面的示例演示如何使用`ISDATE`要测试的字符串是否是有效**datetime**。  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    PRINT 'VALID'  
ELSE  
    PRINT 'INVALID';  
```  
  
### <a name="b-showing-the-effects-of-the-set-dateformat-and-set-language-settings-on-return-values"></a>B. 显示 SET DATEFORMAT 和 SET LANGUAGE 设置对返回值的影响  
 下面的语句显示了作为 `SET DATEFORMAT` 和 `SET LANGUAGE` 设置的结果返回的值。  
  
```  
/* Use these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
/* Expression in mdy dateformat */  
SELECT ISDATE('04/15/2008'); --Returns 1.  
/* Expression in mdy dateformat */  
SELECT ISDATE('04-15-2008'); --Returns 1.   
/* Expression in mdy dateformat */  
SELECT ISDATE('04.15.2008'); --Returns 1.   
/* Expression in myd  dateformat */  
SELECT ISDATE('04/2008/15'); --Returns 1.  
  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET DATEFORMAT dmy;  
SELECT ISDATE('15/04/2008'); --Returns 1.  
SET DATEFORMAT dym;  
SELECT ISDATE('15/2008/04'); --Returns 1.  
SET DATEFORMAT ydm;  
SELECT ISDATE('2008/15/04'); --Returns 1.  
SET DATEFORMAT ymd;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET LANGUAGE English;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET LANGUAGE Hungarian;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET LANGUAGE Swedish;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET LANGUAGE Italian;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
/* Return to these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-isdate-to-test-for-a-valid-datetime-expression"></a>C. 使用 ISDATE 测试是否为有效的 datetime 表达式  
 下面的示例演示如何使用`ISDATE`要测试的字符串是否是有效**datetime**。  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    SELECT 'VALID';  
ELSE  
    SELECT 'INVALID';  
```  
  
## <a name="see-also"></a>另请参阅  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


