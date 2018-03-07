---
title: "TRY_PARSE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_PARSE_TSQL
- TRY_PARSE
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_PARSE function
ms.assetid: 292bac1d-edd8-468c-8ff1-8c7de625bc55
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b26f46431909dd4fbfaa820db8c3869333f555d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="tryparse-transact-sql"></a>TRY_PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，返回表达式的结果（已转换为请求的数据类型）；如果强制转换失败，则返回 Null。 TRY_PARSE 仅用于从字符串转换为日期/时间和数字类型。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
TRY_PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>参数  
 *string_value*  
 **nvarchar （4000)**值，该值表示要将解析到指定的数据类型的格式化的值。  
  
 *string_value*必须是有效的表示形式的请求的数据类型或 TRY_PARSE 返回为 null。  
  
 *data_type*  
 表示结果的所请求数据类型的文本。  
  
 *区域性*  
 标识在其中的区域性的可选字符串*string_value*设置的格式。  
  
 如果*区域性*既未提供参数，则使用当前会话的语言。 此语言使用 SET LANGUAGE 语句隐式或显式设置。 *区域性*接受任何.NET Framework 中; 支持的区域性并不局限于显式支持的语言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*区域性*自变量无效，分析引发错误。  
  
## <a name="return-types"></a>返回类型  
 返回表达式的结果（已转换为请求的数据类型）；如果强制转换失败，则返回 Null。  
  
## <a name="remarks"></a>注释  
 TRY_PARSE 仅用于从字符串转换为日期/时间和数字类型。 对于一般的类型转换，请继续使用 CAST 或 CONVERT。 请记住，分析字符串值会带来一定的性能开销。  
  
 TRY_PARSE 依赖于 .NET Framework 公共语言运行时 (CLR) 的存在。  
  
 此函数将不会进行远程处理，因为它依赖于 CLR 的存在。 远程处理需要 CLR 的函数会导致在远程服务器上出现错误。  
  
 **有关 data_type 参数的详细信息**  
  
 值*data_type*参数仅限于下表，以及样式中所示的类型。 提供的样式信息有助于确定允许使用哪些类型的模式。 样式的详细信息，请参阅的.NET Framework 文档**System.Globalization.NumberStyles**和**DateTimeStyles**枚举。  
  
|类别|类型|.NET 类型|使用的样式|  
|--------------|----------|---------------|-----------------|  
|数字|bigint|Int64|NumberStyles.Number|  
|数字|int|Int32|NumberStyles.Number|  
|数字|smallint|Int16|NumberStyles.Number|  
|数字|tinyint|Byte|NumberStyles.Number|  
|数字|decimal|Decimal|NumberStyles.Number|  
|数字|numeric|Decimal|NumberStyles.Number|  
|数字|float|双精度|NumberStyles.Float|  
|数字|real|Single|NumberStyles.Float|  
|数字|smallmoney|Decimal|NumberStyles.Currency|  
|数字|money|Decimal|NumberStyles.Currency|  
|日期和时间|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期和时间|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期和时间|datetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期和时间|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期和时间|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期和时间|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
  
 **区域性参数有关的详细信息**  
  
 下表显示从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言到 .NET Framework 区域性的映射。  
  
|完全名称|别名|LCID|特定区域性|  
|---------------|-----------|----------|----------------------|  
|us_english|英语|2052|zh-CN|  
|Deutsch|德语|1031|de-DE|  
|Français|法语|1036|fr-FR|  
|日本語|日语|1041|ja-JP|  
|Dansk|丹麦语|1030|da-DK|  
|Español|西班牙语|3082|es-ES|  
|Italiano|意大利语|1040|it-IT|  
|Nederlands|荷兰语|1043|nl-NL|  
|Norsk|挪威语|2068|nn-NO|  
|Português|葡萄牙语|2070|pt-PT|  
|Suomi|芬兰语|1035|fi|  
|Svenska|瑞典语|1053|sv-SE|  
|čeština|捷克语|1029|Cs-CZ|  
|magyar|匈牙利语|1038|Hu-HU|  
|polski|波兰语|1045|Pl-PL|  
|română|罗马尼亚语|1048|Ro-RO|  
|hrvatski|克罗地亚语|1050|hr-HR|  
|slovenčina|斯洛伐克语|1051|Sk-SK|  
|slovenski|斯洛文尼亚语|1060|Sl-SI|  
|ελληνικά?|希腊语|1032|El-GR|  
|български|保加利亚语|1026|bg-BG|  
|русский|俄语|1049|Ru-RU|  
|Türkçe|土耳其语|1055|Tr-TR|  
|British|英国英语|2057|en-GB|  
|eesti|爱沙尼亚语|1061|Et-EE|  
|latviešu|拉脱维亚语|1062|lv-LV|  
|lietuvių|立陶宛语|1063|lt-LT|  
|Português (Brasil)|葡萄牙语（巴西）|1046|pt-BR|  
|繁體中文|繁体中文|1028|zh-TW|  
|한국어|朝鲜语|1042|Ko-KR|  
|简体中文|简体中文|2052|zh-CN|  
|阿拉伯语|阿拉伯语|1025|ar-SA|  
|ไทย|泰国语|1054|Th-TH|  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example-of-tryparse"></a>A. TRY_PARSE 的简单示例  
  
```  
SELECT TRY_PARSE('Jabberwokkie' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-detecting-nulls-with-tryparse"></a>B. 检测 TRY_PARSE 的 Null 值  
  
```  
SELECT  
    CASE WHEN TRY_PARSE('Aragorn' AS decimal USING 'sr-Latn-CS') IS NULL  
        THEN 'True'  
        ELSE 'False'  
END  
AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
True  
  
(1 row(s) affected)  
```  
  
### <a name="c-using-iif-with-tryparse-and-implicit-culture-setting"></a>C. 将 IIF 用于 TRY_PARSE 和隐式区域性设置  
  
```  
SET LANGUAGE English;  
SELECT IIF(TRY_PARSE('01/01/2011' AS datetime2) IS NULL, 'True', 'False') AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
False  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [分析 &#40;Transact SQL &#41;](../../t-sql/functions/parse-transact-sql.md)   
 [转换函数 &#40;Transact SQL &#41;](../../t-sql/functions/conversion-functions-transact-sql.md)   
 [TRY_CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
