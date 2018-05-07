---
title: ClosingPeriod (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CLOSINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- ClosingPeriod function
ms.assetid: ae709017-219d-43e1-a98a-a85bd365b4cd
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 43094cc0934c516a871e249fd9bbdc22d0c4bf12
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定成员在指定级别的后代中的最后一个同级成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 此函数主要用于具有 Time 类型的维度，但也可用于任何维度。  
  
-   如果指定一个级别表达式，则**ClosingPeriod**函数使用包含指定的级别，并返回最后一个同级的后代中的指定级别的默认成员的维度。  
  
-   如果指定了一个级别表达式和一个成员表达式， **ClosingPeriod**函数将返回指定成员在指定级别的后代中的最后一个同级。  
  
-   如果指定既不是级别表达式，也不是成员表达式，则**ClosingPeriod**函数使用的默认级别和维度成员 （如果有） 的时间类型的多维数据集中。  
  
 **ClosingPeriod**函数等同于以下的 MDX 语句：  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`中创建已分区表或索引。  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)函数是类似于**ClosingPeriod**函数，只不过**OpeningPeriod**函数将返回而不是最后一个同级的第一个同级。  
  
## <a name="examples"></a>示例  
 下面的示例返回 Date 维度（具有 Time 语义类型）的“FY2007”成员的默认度量值。 返回此成员是因为：“会计年度”级别是“(全部)”级别的第一个后代；“Fiscal”层次结构是默认层次结构（因为它是层次结构集合中的第一个用户定义的层次结构）；而且“FY 2007”成员是此层次结构在此级别处的最后一个同级成员。  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回“November 30, 2006”成员在 Date.Date 属性层次结构的 Date.Date.Date 级别处的默认度量值。 此成员是 Date.Date 属性层次结构中“(全部)”级别的后代的最后一个同级成员。  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 下例返回“December, 2003”成员的默认度量值。该成员是用户定义的层次结构“Calendar”中年份级别成员“2003”的后代的最后一个同级成员。  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回“June, 2003”成员的默认度量值，该成员是用户定义的层次结构“Fiscal”中年份级别成员“2003”的后代的最后一个同级成员。  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
