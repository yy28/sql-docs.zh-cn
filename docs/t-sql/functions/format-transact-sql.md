---
title: "格式 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs: TSQL
helpviewer_keywords: FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46c7becb151b1942b411aefe337717172f207bb9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中以指定的格式和可选的区域性格式化的值。 使用 FORMAT 函数将日期/时间和数字值格式化为识别区域设置的字符串。 对于一般的数据类型转换，请使用 CAST 或 CONVERT。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>参数  
 *值*  
 支持格式化的数据类型的表达式。 有关有效类型的列表，请参阅下面“备注”部分中的表。  
  
 *format*  
 **nvarchar**格式模式。  
  
 *格式*参数必须包含一个有效的.NET Framework 格式字符串，为标准格式字符串 （例如，"C"或"D"），或作为自定义字符的模式的日期和数字值 (例如，"MMMM DD，yyyy (dddd)"). 不支持组合格式。 这些格式设置模式的完整说明，请查阅上格式设置的常规字符串、 自定义日期和时间格式和自定义数字格式的.NET Framework 文档。 很好的起点是主题中，"[格式类型](http://go.microsoft.com/fwlink/?LinkId=211776)。"  
  
 *culture*  
 可选**nvarchar**指定区域性的自变量。  
  
 如果*区域性*既未提供参数，则使用当前会话的语言。 可以使用 SET LANGUAGE 语句隐式或显式设置此语言。 *区域性*接受任何作为自变量;.NET Framework 支持的区域性并不局限于显式支持的语言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*区域性*自变量无效，格式将引发错误。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**或 null  
  
 返回值的长度由*格式*。  
  
## <a name="remarks"></a>注释  
 格式错误对于返回 NULL 以外*区域性*不*有效*。 例如，如果在指定的值返回 NULL*格式*无效。  
 
 FORMAT 函数具有不确定性。   
  
 格式依赖于存在的.NET Framework 公共语言运行时 (CLR)。  
  
 此函数不能为进行远程处理，因为它依赖于 CLR 的存在状态。 远程服务器上，远程处理某个函数需要 CLR，可能会导致错误。  
  
 格式依赖于 CLR 格式设置规则，规定冒号和期间必须进行转义。 因此，当的格式字符串 （第二个参数） 时，才包含冒号或句点、 冒号或段必须与输入值时的反斜杠转义 （第一个参数） 属于**时间**数据类型。 请参阅[时间数据类型与D.格式](#ExampleD)。  
  
 下表列出的可接受的数据类型*值*及其.NET Framework 映射等效类型的自变量。  
  
|类别|类型|.NET 类型|  
|--------------|----------|---------------|  
|数字|bigint|Int64|  
|数字|int|Int32|  
|数字|smallint|Int16|  
|数字|tinyint|Byte|  
|数字|decimal|SqlDecimal|  
|数字|numeric|SqlDecimal|  
|数字|float|双精度|  
|数字|real|Single|  
|数字|smallmoney|Decimal|  
|数字|money|Decimal|  
|日期和时间|date|DateTime|  
|日期和时间|time|TimeSpan|  
|日期和时间|datetime|DateTime|  
|日期和时间|smalldatetime|DateTime|  
|日期和时间|datetime2|DateTime|  
|日期和时间|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-format-example"></a>A. 简单 FORMAT 示例  
 下面的示例返回针对不同区域性格式化的简单日期。  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';   
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. 使用自定义格式字符串执行 FORMAT  
 以下示例通过指定自定义格式显示格式数值。 该示例假定当前日期是 2012 年 9 月 27 日。 有关这些及其他自定义格式的详细信息，请参阅[自定义数字格式字符串](http://msdn.microsoft.com/library/0c899ak8.aspx)。  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. 用于数值类型的 FORMAT  
 下面的示例返回从 5 行**Sales.CurrencyRate**表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。 列**EndOfDateRate**存储类型为**money**表中。 在本示例中，该列以非格式化形式返回，然后通过指定 .NET 数字格式、常规格式和货币格式类型进行格式化。 有关这些及其他数值格式的详细信息，请参阅[标准数字格式字符串](http://msdn.microsoft.com/library/dwhawy9k.aspx)。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 此示例指定了德语区域性 (de-de)。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
###  <a name="ExampleD"></a> D. 带有时间数据类型格式  
 格式在这些情况下返回 NULL，因为`.`和`:`未转义。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 格式返回的格式化的字符串，因为`.`和`:`都会经过转义。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>另请参阅  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
