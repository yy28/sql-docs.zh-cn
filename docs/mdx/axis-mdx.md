---
title: "轴 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AXIS
dev_langs:
- kbMDX
helpviewer_keywords:
- Axis function
ms.assetid: a3a60a1e-e266-4fa1-ae13-bae73544de33
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95a1d7f16c7f30f2a118820414994a615090d96c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="axis-mdx"></a>Axis (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定轴上的元组集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>参数  
 *Axis_Number*  
 指定轴号的有效数值表达式。  
  
## <a name="remarks"></a>備註  
 **轴**函数使用轴的从零开始的位置在轴上返回的元组集。 例如，`Axis(0)` 返回 COLUMNS 轴，`Axis(1)` 返回 ROWS 轴，等等。 **轴**函数不能在筛选器轴上。 此函数可用于使计算成员识别正在运行的查询的上下文。 例如，您可能需要一个计算成员，该成员仅提供行轴上所选那些成员的总和。 它还可用于使一个轴的定义依赖于另一个轴的定义。 例如，根据列轴上第一项的值对行轴的内容进行排序。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

