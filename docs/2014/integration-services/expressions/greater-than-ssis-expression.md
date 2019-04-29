---
title: '&gt;（大于）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: 2e22efa3-eeb1-4984-a95c-9bccdcf98892
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 52df62d9a69d57b95c3e3f4fa9a6e75599925953
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898019"
---
# <a name="gt-greater-than-ssis-expression"></a>&gt;（大于）（SSIS 表达式）
  通过比较来确定第一个表达式是否大于第二个表达式。 在执行比较前表达式计算器会自动转换多种数据类型。  
  
> [!NOTE]  
>  该运算符不支持对使用 DT_TEXT、DT_NTEXT 或 DT_IMAGE 数据类型的表达式进行比较。  
  
 但是，某些数据类型要求表达式包括显式转换，才能成功进行计算。 有关数据类型之间的合法转换的详细信息，请参阅[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
expression1 > expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *expression1、expression2*  
 为任意有效的表达式。 两个表达式都必须包含可隐式转换的数据类型。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>备注  
 如果比较中的任一表达式为空，则比较结果为空。 如果两个表达式都为空，则结果为空。  
  
 表达式集， *expression1* 和 *expression2*，必须遵守下列规则之一：  
  
-   **Numeric**   *expression1* 和 *expression2* 必须为数值数据类型。 数据类型的交集必须为数值数据类型，该类型在表达式计算器执行隐式数值转换的规则中指定。 两个数值数据类型的交集不能为空。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
-   **Character** ： *expression1* 和 *expression2* 的计算结果必须为 DT_STR 或 DT_WSTR 数据类型。 两个表达式的计算结果可以为不同的字符串数据类型。  
  
    > [!NOTE]  
    >  字符串比较区分大小写、重音、假名和全半角。  
  
-   **“日期”、“时间”或“日期/时间”**：expression1 和 expression2 的计算结果必须为下面的数据类型之一：DT_DBDATE、DT_DATE、DT_DBTIME、DT_DBTIME2、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAPMOFFSET 或 DT_FILETIME。  
  
    > [!NOTE]  
    >  系统不支持对计算结果为时间数据类型的表达式和计算结果为日期或日期/时间数据类型的表达式进行比较。 否则系统会生成错误。  
  
     在对表达式进行比较时，系统会按照所列出的顺序应用下面的转换规则：  
  
    -   当两个表达式的计算结果为同一个数据类型时，则会执行该数据类型的比较。  
  
    -   如果一个表达式是 DT_DBTIMESTAMPOFFSET 数据类型，则另一个表达式会隐式转换为 DT_DBTIMESTAMPOFFSET，并执行 DT_DBTIMESTAMPOFFSET 比较。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
    -   如果一个表达式是 DT_DBTIMESTAMP2 数据类型，则另一个表达式会隐式转换为 DT_DBTIMESTAMP2，并执行 DT_DBTIMESTAMP2 比较。  
  
    -   如果一个表达式是 DT_DBTIME2 数据类型，则另一个表达式会隐式转换为 DT_DBTIME2，并执行 DT_DBTIME2 比较。  
  
    -   如果一个表达式是 DT_DBTIMESTAMPOFFSET、DT_DBTIMESTAMP2 或 DT_DBTIME2 以外的类型，那么，在对表达式进行比较之前，会将它们转换为 DT_DBTIMESTAMP 数据类型。  
  
     在对表达式进行比较时，系统会进行如下假设：  
  
    -   如果每个表达式的数据类型都包含小数秒，则系统会假设对于小数秒位数最少的数据类型，用零填充其余位。  
  
    -   如果每个表达式都是日期数据类型，但是只有一个表达式具有时区偏移量，系统会假设没有时区偏移量的日期数据类型采用的是协调世界时 (UTC)。  
  
 有关数据类型的详细信息，请参阅 [Integration Services Data Types](../data-flow/integration-services-data-types.md)。  
  
## <a name="expression-examples"></a>表达式示例  
 如果当前日期早于 2003 年 7 月 4 日，则此示例的计算结果为 TRUE。 有关详细信息，请参阅 [GETDATE（SSIS 表达式）](getdate-ssis-expression.md)。  
  
```  
"7/4/2003" > GETDATE()  
```  
  
 如果 **ListPrice** 列中的值大于 500，则此示例的计算结果为 TRUE。  
  
```  
ListPrice > 500  
```  
  
 此示例使用了变量 **LPrice**。 如果 **LPrice** 的值大于 500，则此示例的计算结果为 TRUE。 该变量的数据类型必须为数值以便分析表达式。  
  
```  
@LPrice > 500  
```  
  
## <a name="see-also"></a>请参阅  
 [>（小于）（SSIS 表达式）](less-than-ssis-expression.md)   
 [>=（大于或等于）（SSIS 表达式）](greater-than-or-equal-to-ssis-expression.md)   
 [<=（小于或等于）（SSIS 表达式）](less-than-or-equal-to-ssis-expression.md)   
 [==（等于）（SSIS 表达式）](equal-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
