---
title: 支持的数据类型 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 585ce68402e8922f6c9629d8f4e8cd517218106f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067274"
---
# <a name="data-types-supported-ssas-tabular"></a>支持的数据类型（SSAS 表格）
  本文说明可在表格模型中使用的数据类型，并且论述在数据分析表达式 (DAX) 公式中计算或使用数据时数据类型的隐式转换。  
  
 本文包含以下各节：  
  
-   [在表格模型中使用的数据类型](#bkmk_data_types)  
  
-   [DAX 公式中的隐式和显式数据类型转换](#bkmk_implicit)  
  
-   [空白、空字符串和零值的处理](#bkmk_hand_blanks)  
  
##  <a name="bkmk_data_types"></a> 在表格模型中使用的数据类型  
 支持以下数据类型。 当您在公式中导入数据或者使用某一值时，即使原始数据源包含不同的数据类型，该数据也转换为以下数据类型之一。 从公式得出的值也使用这些数据类型。  
  
 通常，实施这些数据类型以便在计算列中实现精确的计算，并且相同的限制将应用于模型中的其余数据以便保持一致性。  
  
 用于数字、货币、日期和时间的格式应遵循在用于处理模型数据的客户端上指定的区域设置的格式。 您可以使用模型中的格式设置选项控制显示值的方式。  
  
||||  
|-|-|-|  
|模型中的数据类型|DAX 中的数据类型|Description|  
|整数|一个 64 位（八字节）整数值 <sup>1、2</sup>|没有小数位的数字。 整数可以是正数或负数，但必须是介于 -9,223,372,036,854,775,808 (-2^63) 和 9,223,372,036,854,775,807 (2^63-1) 之间的整数。|  
|小数|一个 64 位（八字节）实数 <sup>1、2</sup>|实数是可具有小数位的数字。 实数涵盖很广范围的值：<br /><br /> 从 -1.79E +308 到 -2.23E -308 的负值<br /><br /> 零<br /><br /> 从 2.23E -308 到 1.79E + 308 的正值<br /><br /> 但是，有效位数限制为 17 个小数位。|  
|Boolean|Boolean|True 或 False 值。|  
|Text|String|一个 Unicode 字符数据字符串。 可以是字符串，或以文本格式表示的数字或日期。|  
|Date|日期/时间|采用接受的日期-时间表示形式的日期和时间。<br /><br /> 有效值是 1900 年 3 月 1 日后的所有日期。|  
|Currency|Currency|货币数据类型允许值介于 -922,337,203,685,477.5808 到 922,337,203,685,477.5807 之间，并且具有四个小数位的固定精度。|  
|不可用|空白|空白是 DAX 中的一种数据类型，表示并替代 SQL 中的 Null。 您可以通过使用 BLANK 函数创建空白，并通过使用逻辑函数 ISBLANK 测试是否存在空白。|  
  
 <sup>1</sup> DAX 公式不支持比表中列出的较小的数据类型。  
  
 <sup>2</sup>如果尝试导入具有非常大数值数据，导入可能会失败并出现以下错误：  
  
 内存中数据库错误：\<列名称 > 的列\<表名称 > 表包含一个值 1.7976931348623157 e + 308，这不受支持。 操作已取消。  
  
 此错误是因为模型设计器使用该值来表示 Null 导致的。 下表中的值是上述 Null 值的同义词：  
  
||  
|-|  
|ReplTest1|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 您应该从数据中删除该值并且尝试再次导入。  
  
> [!NOTE]  
>  不能从字符串长度超过 131,072 个字符的 **varchar(max)** 列进行导入。  
  
### <a name="table-data-type"></a>表数据类型  
 此外，DAX 使用“表”  数据类型。 DAX 在许多函数中都使用此数据类型，如在聚合和时间智能计算中。 某些函数要求对表的引用；其他函数返回可用作对其他函数的输入的表。 在要求表作为输入的某些函数中，您可以指定计算结果为表的表达式；对于某些函数，要求对基表的引用。 有关特定函数的要求的信息，请参阅 [DAX 函数引用](https://msdn.microsoft.com/library/ee634396.aspx)。  
  
##  <a name="bkmk_implicit"></a> DAX 公式中的隐式和显式数据类型转换  
 每个 DAX 函数都对用作输入和输出的数据类型具有特定的要求。 例如，某些函数要求将整数用于某些参数，将日期用于其他参数；其他一些函数则要求文本或表。  
  
 如果列中您指定为参数的数据与函数所要求的数据类型不兼容，则在许多情况下 DAX 都会返回错误。 但是，只要可能，DAX 都会尝试隐式将数据转换为所需的数据类型。 例如：  
  
-   作为一个字符串，可以键入一个数字，例如"123，"。 DAX 将对字符串进行分析并且尝试将其指定为数字数据类型。  
  
-   您可以将 TRUE + 1 并且获取结果 2，因为 TRUE 隐式转换为数字 1 并且将执行运算 1+1。  
  
-   如果您将两列中的值相加，并且一个值表示为文本 ("12")，另一个值表示为数字 (12)，则 DAX 会隐式将字符串转换为数字，然后执行加法以得到数值结果。 下面的表达式返回 44: = "22" + 22  
  
-   如果你尝试连接两个数字，则 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 外接程序会将它们显示为字符串，然后执行连接。 下面的表达式返回 "1234": = 12 & 34  
  
 下表总结了在公式中执行的隐式数据类型转换。 通常，语义模型设计器在行为上类似于 Microsoft Excel，在指定操作要求时将尽可能执行隐式转换。  
  
### <a name="table-of-implicit-data-conversions"></a>隐式数据转换表  
 执行的转换类型由运算符确定，运算符在执行请求的运算前转换它要求的值。 这些表列出了运算符，并且在与相交行中的数据类型搭配时指示对列中的每种数据类型执行的转换。  
  
> [!NOTE]  
>  这些表中不包含文本数据类型。 在数字表示为文本格式时，在某些情况下，模型设计器将尝试确定数字类型并且将其表示为数字。  
  
#### <a name="addition-"></a>加 (+)  
  
||||||  
|-|-|-|-|-|  
|运算符 (+)|整数|货币|real|日期/时间|  
|整数|整数|货币|real|日期/时间|  
|货币|货币|货币|real|日期/时间|  
|real|real|real|real|日期/时间|  
|日期/时间|日期/时间|日期/时间|日期/时间|日期/时间|  
  
 例如，如果某一实数在加法运算中与货币数据结合使用，则两个值都转换为 REAL，并且结果返回为 REAL。  
  
#### <a name="subtraction--"></a>减 (-)  
 在下表中，行标题是被减数（左侧），列标题是减数（右侧）。  
  
||||||  
|-|-|-|-|-|  
|运算符 (-)|整数|货币|real|日期/时间|  
|整数|整数|货币|real|real|  
|货币|货币|货币|real|real|  
|real|real|real|real|real|  
|日期/时间|日期/时间|日期/时间|日期/时间|日期/时间|  
  
 例如，如果某一日期用于采用任何其他数据类型的减法运算中，则两个值都转换为日期，并且返回值也是日期。  
  
> [!NOTE]  
>  表格模型还支持一元运算符 -（负号），但此运算符不能更改操作数的数据类型。  
  
#### <a name="multiplication-"></a>乘 (*)  
  
||||||  
|-|-|-|-|-|  
|运算符 (*)|整数|货币|real|日期/时间|  
|整数|整数|货币|real|整数|  
|货币|货币|real|货币|货币|  
|real|real|货币|real|real|  
  
 例如，如果在乘法运算中某一整数与实数结合使用，则两个数字都将转换为实数，并且返回值也是 REAL。  
  
#### <a name="division-"></a>除 (/)  
 在下表中，行标题是分子，列标题是分母。  
  
||||||  
|-|-|-|-|-|  
|运算符 (/)<br /><br /> （行/列）|整数|货币|real|日期/时间|  
|整数|real|货币|real|real|  
|货币|货币|real|货币|real|  
|real|real|real|real|real|  
|日期/时间|real|real|real|real|  
  
 例如，如果某一整数在除法运算中与某一货币值一起使用，则两个值都转换为实数，并且结果也是实数。  
  
#### <a name="comparison-operators"></a>比较运算符  
 在比较表达式中，布尔值被视作大于字符串值，字符串值被视作大于数值或者日期/时间值，数值和日期/时间值被视作具有相同排名。 对布尔值或字符串值不执行隐式转换；BLANK 或空白值根据其他比较值的数据类型转换为 0/""/false。  
  
 下面的 DAX 表达式说明此行为：  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")`，返回 `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")`，返回 `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")`，返回 `"Expression is false"`  
  
 如下表所述，为数字或日期/时间类型执行隐式转换：  
  
||||||  
|-|-|-|-|-|  
|比较运算符|整数|货币|real|日期/时间|  
|整数|整数|货币|real|real|  
|货币|货币|货币|real|real|  
|real|real|real|real|real|  
|日期/时间|real|real|real|日期/时间|  
  
##  <a name="bkmk_hand_blanks"></a> 空白、空字符串和零值的处理  
 DAX 处理零值、Null 和空字符串的方式不同于 Microsoft Excel 和 SQL Server。 本节描述这些差异，并描述如何处理这些数据类型。  
  
 务必要记住的是，空白值、空单元或缺失值全都由同一新的值类型表示，即 BLANK。 在运算（例如加法或串联）中处理空白的方式取决于各个函数。 您也可以通过使用 BLANK 函数生成空白，或者通过使用 ISBLANK 函数测试是否有空白。 在语义模型内并不支持数据库 Null，并且在 DAX 公式中引用包含 Null 值的列时，Null 将隐式转换为空白。  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>定义空白、Null 和空字符串  
 下表汇总了 DAX 和 Microsoft Excel 之间在处理空白的方式上的差异。  
  
||||  
|-|-|-|  
|表达式|DAX|“导出”|  
|BLANK + BLANK|空白|0（零）|  
|BLANK +5|5|5|  
|BLANK * 5|空白|0（零）|  
|5/BLANK|无穷|错误|  
|0/BLANK|NaN|错误|  
|BLANK/BLANK|空白|错误|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|空白|错误|  
|BLANK AND BLANK|空白|错误|  
  
 有关特定函数或运算符如何处理空白的详细信息，请参阅 [DAX 函数引用](https://msdn.microsoft.com/library/ee634396.aspx)一节中关于各 DAX 函数的单独主题。  
  
## <a name="see-also"></a>请参阅  
 [数据源（SSAS 表格）](../data-sources-ssas-tabular.md)   
 [导入数据（SSAS 表格）](../import-data-ssas-tabular.md)  
  
  
