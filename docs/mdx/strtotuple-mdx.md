---
title: StrToTuple (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35cd9cf849ce35bf82c839f0bbeeb657a75e990c
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743226"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  返回多维表达式 (MDX) 格式的字符串指定的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Specification*  
 直接或间接指定元组的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **StrToTuple**函数返回指定的集。 **StrToTuple**函数通常用于与用户定义的函数返回元组规范函数的外部函数从回 MDX 语句。  
  
-   如果使用 CONSTRAINED 标志，则元组规范必须包含限定或未限定的成员名称。 此标志通过指定字符串可降低注入攻击的风险。 如果所提供的字符串无法直接解析为限定或未限定的成员名称，将出现以下错误：“违反了 STRTOTUPLE 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   如果未使用 CONSTRAINED 标志，则指定的元组可以解析为有效的 MDX 表达式以返回元组。  
  
## <a name="examples"></a>示例  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含有效的 MDX 元组表达式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含了 CONSTRAINED 标志所需的限定成员名称。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含有效的 MDX 元组表达式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回因 CONSTRAINED 标志而引起的错误。 虽然所提供的元组规范包含有效的 MDX 元组表达式，但是 CONSTRAINED 标志要求元组规范包含限定或未限定的成员名称。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
