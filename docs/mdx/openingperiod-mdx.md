---
title: OpeningPeriod (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- OpeningPeriod function
ms.assetid: bebf55cf-e5c6-42b1-98f2-1d6e54093d4c
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6f0ceb660009214e341c423261620d749e3ed1c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定级别（也可以是指定成员）的后代中的第一个同级。  
  
## <a name="syntax"></a>语法  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 该函数主要用于时间维度，但是也可以用于任何维度。  
  
-   如果指定一个级别表达式，则**OpeningPeriod**函数使用的层次结构，包含指定的级别，并返回在指定的级别的默认成员的后代的第一个同级。  
  
-   如果指定了一个级别表达式和一个成员表达式， **OpeningPeriod**函数返回的第一个同级元素的后代中的指定成员在层次结构包含指定的级别中指定的级别。  
  
-   如果指定既不是级别表达式，也不是成员表达式， **OpeningPeriod**函数使用了一个类型为时间的默认级别和维度成员。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函数是类似于**OpeningPeriod**函数，只不过**ClosingPeriod**函数将返回而不是第一个同级的最后一个同级。  
  
## <a name="examples"></a>示例  
 下面的示例将返回 Date 维度（Time 类型）FY2002 成员的默认度量值。 返回该成员是因为 Fiscal Year 级别是 [All] 级别的第一个后代，Fiscal 层次结构为默认层次结构是由于 Fiscal 层次结构是层次结构集合中第一个用户定义的层次结构，而且 FY2002 成员是该层次结构中该级别上的第一个同级。  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 下例将返回 Date.Date 属性层次结构 Date.Date.Date 级别上“July 1, 2001”成员的默认度量值。 该成员是 Date.Date 属性层次结构中 [All] 级别后代的第一个同级成员。  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例将返回“January, 2003”成员的默认度量值，该成员是 Calendar 用户定义层次结构中年度级别上 2003 成员后代的第一个同级成员。  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例将返回“July, 2002”成员的默认度量值，该成员是 Fiscal 用户定义层次结构中年度级别上 2003 成员后代的第一个同级成员。  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
