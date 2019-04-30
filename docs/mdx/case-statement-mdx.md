---
title: CASE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fb53db11e9c7ec816299d1541d27e962ab8650df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181591"
---
# <a name="case-statement-mdx"></a>CASE 语句 (MDX)


  允许您有条件地从多次比较中返回特定值。 有两种类型的 Case 语句：  
  
-   简单 Case 语句将某个表达式与一组简单表达式进行比较，以返回特定的值。  
  
-   搜索 Case 语句计算一组布尔表达式，以返回特定的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>参数  
 *input_expression*  
 解析为标量值的多维表达式 (MDX)。  
  
 *when_expression*  
 一个指定标量值*input_expression*计算时，此操作时的计算结果为 true，则返回的标量值*else_result_expression*。  
  
 *when_true_result_expression*  
 当 WHEN 子句计算结果为 True 时返回的标量值。  
  
 *else_result_expression*  
 当没有任何 WHEN 子句的计算结果为 True 时返回的标量值。  
  
 *Boolean_expression*  
 计算结果为标量值的 MDX 表达式。  
  
## <a name="remarks"></a>备注  
 如果没有 ELSE 子句，而且所有 WHEN 子句的计算结果都为 False，则结果是空单元。  
  
## <a name="simple-case-expression"></a>简单 Case 表达式  
 MDX 计算简单 case 表达式通过解决*input_expression*为标量值。 该标量值进行比较的标量值*when_expression*。 如果两个标量值匹配，CASE 语句返回的值*when_true_expression*。 如果这两个标量值不匹配，则计算下一个 WHEN 子句。 如果所有的 WHEN 子句计算结果为 false，值*else_result_expression*从 ELSE 子句，如果有，则返回。  
  
 在下例中，对几个 WHEN 子句计算 Reseller Order Count 度量值，并且基于每年的 Reseller Order Count 度量值的值返回一个结果。 不匹配标量值中指定的 Reseller Order Count 值*when_expression* WHEN 子句的标量值中*else_result_expression*返回。  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>Case 搜索表达式  
 若要使用 Case 表达式执行更为复杂的计算，请使用 Case 搜索表达式。 使用此搜索表达式的变体可以计算输入表达式是否位于一个值范围内。 MDX 按 WHEN 子句出现在 CASE 语句中的顺序计算这些子句。  
  
 在以下示例中，计算 Reseller Order Count 度量值针对指定*Boolean_expression*为每个 WHEN 子句。 根据每年的 Reseller Order Count 度量值的值返回一个结果。 因为按照 WHEN 子句出现的顺序计算这些子句，所以可简单地将所有大于 6 的值赋值为“VERY LARGE”，而无需显式地指定每个值。 未指定 WHEN 子句的标量值中的 Reseller Order Count 值*else_result_expression*返回。  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写语句 (MDX)](../mdx/mdx-scripting-statements-mdx.md)  
  
  
