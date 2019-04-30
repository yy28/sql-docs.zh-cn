---
title: OpeningPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 01144d6a82319b7853ae60f901a5fc0ad3c78d6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277963"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


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
  
## <a name="remarks"></a>备注  
 该函数主要用于时间维度，但是也可以用于任何维度。  
  
-   如果指定了级别表达式，则**OpeningPeriod**函数使用的层次结构，包含指定的级别，并返回指定级别上的默认成员的后代中的第一个同级。  
  
-   如果指定了级别表达式和成员表达式， **OpeningPeriod**函数将返回包含指定层次结构中的指定级别上的指定成员的后代中的第一个同级级别。  
  
-   如果指定了级别表达式既不是成员表达式， **OpeningPeriod**函数使用的是类型的时间的默认级别和维度的成员。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函数是类似于**OpeningPeriod**函数，不同之处在于**ClosingPeriod**函数返回的最后一个同级而不是第一个同级。  
  
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
  
## <a name="see-also"></a>请参阅  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
