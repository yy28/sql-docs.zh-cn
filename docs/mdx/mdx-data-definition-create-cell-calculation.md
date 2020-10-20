---
description: MDX 数据定义 - CREATE CELL CALCULATION
title: " (MDX) 创建单元计算语句 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 94f2a2286b72aac5a8698fad7ba0085f2a6ad8d0
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196994"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>MDX 数据定义 - CREATE CELL CALCULATION


  创建计算，以便通过多维表达式 (MDX) 对多维数据集中的一组指定元组求值。  
  
## <a name="syntax"></a>语法  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串。  
  
 *Calculation_Name*  
 一个提供单元计算名称的有效字符串。  
  
 *Set_Expression*  
 返回一个集的有效 MDX 表达式。  
  
 *字符串*  
 有效的字符串值。  
  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
 *Logical_Expression*  
 有效的 MDX 逻辑表达式。  
  
 *整数*  
 有效的整数值。  
  
 *Calculation_Name*  
 一个提供单元计算属性名称的有效字符串。  
  
 *Scalar_Expression*  
 有效的 MDX 标量表达式。  
  
## <a name="remarks"></a>备注  
 通过使用计算单元，客户端应用程序就可以指定一组特定单元的汇总值，而不必像在自定义汇总公式或计算成员中一样指定所有单元的汇总值。 例如，可以指定 `{[Canada],[Time].[2000]}` 所定义的集中的任意单元都允许包含通过公式定义的值。 不在此集中的其他任何单元都按正常方式计算。  
  
> [!NOTE]  
>  巴科斯-诺尔范式 (BNF) 的 `{*(<comment> | <whitespace> | <newline>)}` 将分析为 `{*}`，以实现向后兼容。  
  
## <a name="see-also"></a>另请参阅  
 [创建 Session-Scoped 计算单元](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [&#40;MDX 创建 Query-Scoped 单元计算&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [在 MDX 中生成单元计算 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [使用单元属性 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [FORMAT_STRING 内容 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [&#40;MDX FORE_COLOR 和 BACK_COLOR 内容&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [Mdx 数据定义语句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
