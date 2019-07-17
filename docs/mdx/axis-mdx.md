---
title: 轴 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa65c1531be29273c0a838b978109bbd1c8a2b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016977"
---
# <a name="axis-mdx"></a>Axis (MDX)


  返回指定轴上的元组集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>参数  
 *Axis_Number*  
 指定轴号的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **轴**函数使用轴的从零开始的位置在轴上返回的元组集。 例如，`Axis(0)` 返回 COLUMNS 轴，`Axis(1)` 返回 ROWS 轴，等等。 **轴**函数不能使用筛选器轴上。 此函数可用于使计算成员识别正在运行的查询的上下文。 例如，您可能需要一个计算成员，该成员仅提供行轴上所选那些成员的总和。 它还可用于使一个轴的定义依赖于另一个轴的定义。 例如，根据列轴上第一项的值对行轴的内容进行排序。  
  
> [!NOTE]  
>  轴只能引用先前的某个轴。 例如，对 COLUMNS 轴求值后，必然出现 `Axis(0)`（例如，在 ROW 或 PAGE 轴上）。  
  
## <a name="examples"></a>示例  
 以下示例查询说明如何使用 Axis 函数：  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 以下示例说明如何在计算成员内使用 Axis 函数：  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
