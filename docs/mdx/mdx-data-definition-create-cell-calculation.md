---
title: CREATE CELL CALCULATION 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e69aa9e3da29abe054aaf272c5fe3ed12172a4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309134"
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
  
 *String*  
 有效的字符串值。  
  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
 *Logical_Expression*  
 有效的 MDX 逻辑表达式。  
  
 *Integer*  
 有效的整数值。  
  
 *Calculation_Name*  
 一个提供单元计算属性名称的有效字符串。  
  
 *Scalar_Expression*  
 有效的 MDX 标量表达式。  
  
## <a name="remarks"></a>备注  
 通过使用计算单元，客户端应用程序就可以指定一组特定单元的汇总值，而不必像在自定义汇总公式或计算成员中一样指定所有单元的汇总值。 例如，可以指定 `{[Canada],[Time].[2000]}` 所定义的集中的任意单元都允许包含通过公式定义的值。 不在此集中的其他任何单元都按正常方式计算。  
  
> [!NOTE]  
>  巴科斯-诺尔范式 (BNF) 的 `{*(<comment> | <whitespace> | <newline>)}` 将分析为 `{*}`，以实现向后兼容。  
  
## <a name="see-also"></a>请参阅  
 [创建会话作用域的计算的单元](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)   
 [创建查询作用域的单元计算 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [构建在 MDX 中的单元格计算&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)   
 [使用单元属性 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [FORMAT_STRING 内容 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [FORE_COLOR 和 BACK_COLOR 内容&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
