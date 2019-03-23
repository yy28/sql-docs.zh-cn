---
title: 表达式中的 Integration Services 数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 99687b8168c16b0ad1ceef5f802b3345038524fe
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378265"
---
# <a name="integration-services-data-types-in-expressions"></a>表达式中的 Integration Services 数据类型
  表达式计算器使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型。 当数据首次进入 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包的数据流中时，数据流引擎将所有列数据转换为 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型，因此，表达式使用的列数据已具有 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型。 有条件拆分和派生列转换中使用的表达式可以引用列，因为它们是包含列数据的数据流的一部分。  
  
## <a name="variables"></a>变量  
 表达式还可以使用变量。 变量具有 Variant 数据类型，表达式计算器在计算表达式前会将变量的数据类型从 Variant 子类型转换为 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型。 变量只能使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型的一个子集。 例如，变量不能使用二进制大型对象块 (BLOB) 数据类型。  
  
 有关 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型和 Variant 数据类型到 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型的映射的详细信息，请参阅 [集成服务数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="literals"></a>文字  
 此外，表达式还可以包含字符串、布尔值和数值。 有关将数值转换为数值 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[文字 (SSIS)](numeric-string-and-boolean-literals.md)。  
  
## <a name="implicit-data-conversion"></a>隐式数据转换  
 当表达式计算器自动将数据从一种数据类型转换为另一种数据类型时，将会发生数据类型的隐式转换。 例如，如果将 `smallint` 与 `int` 比较，则 `smallint` 便会在执行比较前被隐式转换为 `int`。  
  
 当参数和操作数具有不兼容的数据类型时，表达式计算器无法执行隐式数据转换。 此外，表达式计算器无法将任何值隐式转换为布尔值。 相反，参数和操作数必须借助于转换运算符显式转换。 有关详细信息，请参阅[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 以下关系图显示了 BINARY 运算的隐式转换的结果类型。 该表中列和行的交集为二元运算的结果类型，该运算中操作数的类型为左 (From) 和右 (To)。  
  
 ![数据类型之间的隐式数据类型转换](../media/mw-dts-impl-conver-02.gif "Implicit data type conversion between data types")  
  
 有符号整数和无符号整数的交集是可能大于这两者中任何一个的有符号整数。  
  
 操作数可对 String、Date、Boolean 以及其他数据类型进行比较。 在操作数比较两个值之前，表达式计算器会执行某些隐式转换。 表达式计算器始终将字符串文字转换为 DT_WSTR 数据类型，将布尔值文字转换为 DT_BOOL 数据类型。 表达式计算器将引号引起来的所有值都解释为字符串。 数值被转换为数值 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型的一种。  
  
> [!NOTE]  
>  布尔值是逻辑值而非数字。 虽然布尔值在某些环境中可能显示为数字，但它们并非以数字形式存储，而且不同的编程语言以不同的数值表示布尔值，.NET Framework 方法也是如此。  
>   
>  例如，Visual Basic 中可用的转换函数将 `True` 转换为 -1；但是 .NET Framework 中的 `System.Convert.ToInt32` 方法将 `True` 转换为 +1。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 表达式语言将 `True` 转换为 -1。  
>   
>  若要避免错误或意外结果，不应编写依赖 `True` 和 `False` 为特定数值的代码。 如果可能，应将布尔变量的使用限制为与其设计意图对应的逻辑值。  
  
 有关详细信息，请参阅下列主题：  
  
-   [== &#40;等于&#41; &#40;SSIS 表达式&#41;](equal-ssis-expression.md)  
  
-   [!= &#40;不等于&#41; &#40;SSIS 表达式&#41;](unequal-ssis-expression.md)  
  
-   [>（大于）（SSIS 表达式）](greater-than-ssis-expression.md)  
  
-   [>（小于）（SSIS 表达式）](less-than-ssis-expression.md)  
  
-   [>=（大于或等于）（SSIS 表达式）](greater-than-or-equal-to-ssis-expression.md)  
  
-   [&#60;= &#40;小于或等于&#41; &#40;SSIS 表达式&#41;](less-than-or-equal-to-ssis-expression.md)  
  
 使用单个参数的函数将返回与参数具有相同数据类型的结果，但下列情况除外：  
  
-   DAY、MONTH 和 YEAR 接受日期并返回一个整数 (DT_I4) 结果。  
  
-   ISNULL 接受任意 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数据类型的表达式，并返回一个布尔值 (DT_BOOL) 结果。  
  
-   SQUARE 和 SQRT 接受数值表达式，并返回一个非整型数值 (DT_R8) 结果。  
  
 如果参数具有相同的数据类型，则结果即为该类型。 唯一的例外是，如果对两个 DT_DECIMAL 数据类型的值执行二进制操作，则它将返回 DT_NUMERIC 数据类型的结果。  
  
## <a name="requirements-for-data-used-in-expressions"></a>表达式中的数据使用要求  
 表达式计算器支持所有的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型。 但是，根据运算或函数的不同，操作数和参数需要特定的数据类型。 表达式计算器对表达式中使用的数据规定了下列数据类型要求：  
  
-   **“逻辑”** 运算中所用操作数的取值必须为布尔值。 例如，ColumnA > 1&&ColumnB < 2。  
  
-   **“数学”** 运算中所用操作数的取值必须为数值。 例如，23.75 * 4。  
  
-   用在比较运算（如逻辑运算和相等运算）中的操作数的计算结果必须为兼容的数据类型。  
  
     例如，如下示例中的表达式之一使用 DT_DBTIMESTAMPOFFSET 数据类型：  
  
     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`  
  
     系统将表达式 `(DT_DBDATE)"1999-10-12"`转换为 DT_DBTIMESTAMPOFFSET。 此示例的计算结果为 TRUE，因为转换后的表达式变成 "1999-10-12 00:00:00.000 +00:00"，这与另一个表达式 `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`的值不相等。  
  
-   传递给数学函数的参数的取值必须为数值数据类型。 根据函数或运算的不同，可能需要特定的数值数据类型。 例如，HEX 函数需要有符号或无符号整数。  
  
-   传递给字符串函数的参数的计算结果必须为字符数据类型：DT_STR 或 DT_WSTR。 例如，UPPER("flower")。 某些字符串函数（如 SUBSTRING）需要其他整数参数来作为字符串的起始位置和长度。  
  
-   传递给日期和时间函数的参数的取值必须为有效日期。 例如，DAY(GETDATE())。 某些函数（如 DATEADD）需要其他整数参数来作为函数加到某个日期的天数。  
  
 兼具无符号八字节整数和有符号整数的运算需要显式转换才能使结果格式清楚明了。 有关详细信息，请参阅[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 许多运算和函数的结果具有预设的数据类型。 该类型可能是参数的数据类型，也可能是表达式计算器将结果转换到的数据类型。 例如，逻辑或运算符 (||) 的计算结果始终为布尔值，ABS 函数的计算结果是参数的数值数据类型，乘法运算的结果是可完整保存结果的最小数值数据类型。 有关结果的数据类型的详细信息，请参阅[运算符（SSIS 表达式）](operators-ssis-expression.md)和[函数（SSIS 表达式）](functions-ssis-expression.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [在数据流组件中使用表达式](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
  
-   pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](https://go.microsoft.com/fwlink/?LinkId=217683)。  
  
-   social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
  
