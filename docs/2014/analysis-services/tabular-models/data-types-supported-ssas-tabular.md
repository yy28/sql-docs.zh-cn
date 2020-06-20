---
title: 支持的数据类型（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2502b65b1b13f8ed819c138fdfe429390a905a56
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939755"
---
# <a name="data-types-supported-ssas-tabular"></a>支持的数据类型（SSAS 表格）
  本文说明可在表格模型中使用的数据类型，并且论述在数据分析表达式 (DAX) 公式中计算或使用数据时数据类型的隐式转换。  
  
 本文包含以下各节：  
  
-   [在表格模型中使用的数据类型](#bkmk_data_types)  
  
-   [DAX 公式中的隐式和显式数据类型转换](#bkmk_implicit)  
  
-   [空白、空字符串和零值的处理](#bkmk_hand_blanks)  
  
##  <a name="data-types-used-in-tabular-models"></a><a name="bkmk_data_types"></a>表格模型中使用的数据类型  
 支持以下数据类型。 当您在公式中导入数据或者使用某一值时，即使原始数据源包含不同的数据类型，该数据也转换为以下数据类型之一。 从公式得出的值也使用这些数据类型。  
  
 通常，实施这些数据类型以便在计算列中实现精确的计算，并且相同的限制将应用于模型中的其余数据以便保持一致性。  
  
 用于数字、货币、日期和时间的格式应遵循在用于处理模型数据的客户端上指定的区域设置的格式。 您可以使用模型中的格式设置选项控制显示值的方式。  
  
||||  
|-|-|-|  
|模型中的数据类型|DAX 中的数据类型|说明|  
|整数|一个 64 位（八字节）整数值 <sup>1、2</sup>|没有小数位的数字。 整数可以是正数或负数，但必须是介于 -9,223,372,036,854,775,808 (-2^63) 和 9,223,372,036,854,775,807 (2^63-1) 之间的整数。|  
|小数|一个 64 位（八字节）实数 <sup>1、2</sup>|实数是可具有小数位的数字。 实数涵盖很广范围的值：<br /><br /> 从 -1.79E +308 到 -2.23E -308 的负值<br /><br /> 零<br /><br /> 从 2.23E -308 到 1.79E + 308 的正值<br /><br /> 但是，有效位数限制为 17 个小数位。|  
|布尔|布尔|True 或 False 值。|  
|文本|String|一个 Unicode 字符数据字符串。 可以是字符串，或以文本格式表示的数字或日期。|  
|Date|日期/时间|采用接受的日期-时间表示形式的日期和时间。<br /><br /> 有效值是 1900 年 3 月 1 日后的所有日期。|  
|货币|货币|货币数据类型允许值介于 -922,337,203,685,477.5808 到 922,337,203,685,477.5807 之间，并且具有四个小数位的固定精度。|  
|空值|空|空白是 DAX 中的一种数据类型，表示并替代 SQL 中的 Null。 您可以通过使用 BLANK 函数创建空白，并通过使用逻辑函数 ISBLANK 测试是否存在空白。|  
  
 <sup>1</sup> DAX 公式不支持小于表中列出的数据类型。  
  
 <sup>2</sup>如果你尝试导入具有非常大数值的数据，则导入可能会失败，并出现以下错误：  
  
 内存中数据库错误： "" 表的 " \<column name> " 列 \<table name> 包含值 "1.7976931348623157 e + 308"，这是不受支持的。 操作已取消。  
  
 此错误是因为模型设计器使用该值来表示 Null 导致的。 下表中的值是上述 Null 值的同义词：  
  
||  
|-|  
|值|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 您应该从数据中删除该值并且尝试再次导入。  
  
> [!NOTE]  
>  不能从字符串长度超过 131,072 个字符的 **varchar(max)** 列进行导入。  
  
### <a name="table-data-type"></a>表数据类型  
 此外，DAX 使用“表” ** 数据类型。 DAX 在许多函数中都使用此数据类型，如在聚合和时间智能计算中。 某些函数需要引用表；其他函数返回随后可用于输入到其他函数的表。 在某些需要表作为输入的函数中，你可以指定计算结果为表格的表达式；对于一些函数，则需要引用基础表。 有关特定函数的要求的详细信息，请参阅 [DAX 函数引用](/dax/dax-function-reference)。  
  
##  <a name="implicit-and-explicit-data-type-conversion-in-dax-formulas"></a><a name="bkmk_implicit"></a>DAX 公式中的隐式和显式数据类型转换  
 关于用作输入和输出的数据类型，每个 DAX 函数都有特定的要求。 例如，某些函数要求对部分参数使用整数，而其他部分使用日期；另外一些函数则要求使用文本或表。  
  
 如果列中您指定为参数的数据与函数所要求的数据类型不兼容，则在许多情况下 DAX 都会返回错误。 但是，只要可能，DAX 会尝试将数据隐式转换为所需的数据类型。 例如：  
  
-   您可以键入一个数字（例如 "123"）作为字符串。 DAX 将对字符串进行分析并且尝试将其指定为数字数据类型。  
  
-   你可以添加 TRUE+1 并获得结果 2，因为 TRUE 被隐式转换为数字 1，并执行 1+1 的操作。  
  
-   如果在两个列中添加值，其中一个值恰好以文本方式表示 ("12")，而另一个值以数字方式表示 (12)，DAX 会将字符串隐式转换为数字，然后执行加法并获得数值结果。 下面的表达式返回 44: = "22" + 22  
  
-   如果你尝试连接两个数字，则 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 外接程序会将它们显示为字符串，然后执行连接。 下面的表达式返回 "1234": = 12 & 34  
  
 下表总结了在公式中执行的隐式数据类型转换。 通常，语义模型设计器在行为上类似于 Microsoft Excel，在指定操作要求时将尽可能执行隐式转换。  
  
### <a name="table-of-implicit-data-conversions"></a>隐式数据转换表  
 执行的转换的类型由运算符确定，它在执行所请求的操作之前会将值转换为所需的值。 这些表列出了运算符，并指示当其与交叉行内的数据类型配对时，对列中每种数据类型执行的转换。  
  
> [!NOTE]  
>  这些表中不包含文本数据类型。 在数字表示为文本格式时，在某些情况下，模型设计器将尝试确定数字类型并且将其表示为数字。  
  
#### <a name="addition-"></a>加 (+)  
  
||||||  
|-|-|-|-|-|  
|运算符 (+)|INTEGER|CURRENCY|REAL|日期/时间|  
|INTEGER|INTEGER|CURRENCY|REAL|日期/时间|  
|CURRENCY|CURRENCY|CURRENCY|REAL|日期/时间|  
|REAL|REAL|REAL|REAL|日期/时间|  
|日期/时间|日期/时间|日期/时间|日期/时间|日期/时间|  
  
 例如，如果在加法运算中将实数与货币数据结合使用，两个值都会转换为 REAL，并且返回的结果为 REAL。  
  
#### <a name="subtraction--"></a>减法 (–)  
 在下表中，行标题是被减数（左侧），列标题是减数（右侧）。  
  
||||||  
|-|-|-|-|-|  
|运算符 (-)|INTEGER|CURRENCY|REAL|日期/时间|  
|INTEGER|INTEGER|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|CURRENCY|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|日期/时间|日期/时间|日期/时间|日期/时间|日期/时间|  
  
 例如，如果在减法运算中将日期与其他任何数据类型结合使用，两个值都会转换为日期，返回的值也会是日期。  
  
> [!NOTE]  
>  表格模型还支持一元运算符 -（负号），但此运算符不能更改操作数的数据类型。  
  
#### <a name="multiplication-"></a>乘 (*)  
  
||||||  
|-|-|-|-|-|  
|运算符 (*)|INTEGER|CURRENCY|REAL|日期/时间|  
|INTEGER|INTEGER|CURRENCY|REAL|INTEGER|  
|CURRENCY|CURRENCY|REAL|CURRENCY|CURRENCY|  
|REAL|REAL|CURRENCY|REAL|REAL|  
  
 例如，如果在乘法运算中将整数与实数结合使用，两个数字都会转换成为实数，并且返回的值也是 REAL。  
  
#### <a name="division-"></a>除 (/)  
 在下表中，行标题是分子，列标题是分母。  
  
||||||  
|-|-|-|-|-|  
|运算符 (/)<br /><br /> （行/列）|INTEGER|CURRENCY|REAL|日期/时间|  
|INTEGER|REAL|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|REAL|CURRENCY|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|日期/时间|REAL|REAL|REAL|REAL|  
  
 例如，如果在除法运算将整数与货币值结合使用，两个值都会转换为实数，并且结果也是实数。  
  
#### <a name="comparison-operators"></a>比较运算符  
 在比较表达式中，布尔值被视作大于字符串值，字符串值被视作大于数值或者日期/时间值，数值和日期/时间值被视作具有相同排名。 布尔值或字符串值不执行任何隐式转换；BLANK 或空白值会被转换为 0/""/false，具体取决于其他进行比较的值的数据类型。  
  
 下面的 DAX 表达式对此行为进行了说明：  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")`，返回 `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")`，返回 `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")`，返回 `"Expression is false"`  
  
 针对数字或日期/时间类型所执行的隐式转换如下表所述：  
  
||||||  
|-|-|-|-|-|  
|比较运算符|INTEGER|CURRENCY|REAL|日期/时间|  
|INTEGER|INTEGER|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|CURRENCY|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|日期/时间|REAL|REAL|REAL|日期/时间|  
  
##  <a name="handling-of-blanks-empty-strings-and-zero-values"></a><a name="bkmk_hand_blanks"></a>空格、空字符串和零值的处理  
 DAX 处理零值、Null 和空字符串的方式不同于 Microsoft Excel 和 SQL Server。 本节描述这些差异，并描述如何处理这些数据类型。  
  
 务必要记住的是，空白值、空单元或缺失值全都由同一新的值类型表示，即 BLANK。 在运算（例如加法或串联）中处理空白的方式取决于各个函数。 你可以使用 BLANK 函数创建空白，并使用 ISBLANK 函数对其进行测试。 在语义模型内并不支持数据库 Null，并且在 DAX 公式中引用包含 Null 值的列时，Null 将隐式转换为空白。  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>定义空白、Null 和空字符串  
 下表汇总了 DAX 和 Microsoft Excel 之间在处理空白的方式上的差异。  
  
||||  
|-|-|-|  
|表达式|DAX|Excel|  
|BLANK + BLANK|BLANK|0（零）|  
|BLANK +5|5|5|  
|BLANK * 5|BLANK|0（零）|  
|5/BLANK|无穷大|错误|  
|0/BLANK|NaN|错误|  
|空白/空白|BLANK|Error|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|BLANK|Error|  
|BLANK AND BLANK|BLANK|Error|  
  
 有关特定函数或运算符如何处理空白的详细信息，请参阅 [DAX 函数引用](/dax/dax-function-reference)一节中关于各 DAX 函数的单独主题。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的数据源](../data-sources-ssas-tabular.md)   
 [导入数据（SSAS 表格）](../import-data-ssas-tabular.md)  
  
  
