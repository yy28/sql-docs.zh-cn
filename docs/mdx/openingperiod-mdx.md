---
title: OpeningPeriod （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 07f94c3ed850af10120b1de7d95941bc5c90e826
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088224"
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
  
-   如果指定了级别表达式，则**OpeningPeriod**函数将使用包含指定级别的层次结构，并返回默认成员在指定级别的后代中的第一个同级。  
  
-   如果同时指定了级别表达式和成员表达式，则**OpeningPeriod**函数将返回指定成员在包含指定级别的层次结构内指定级别的后代中的第一个同级。  
  
-   如果级别表达式和成员表达式均未指定，则**OpeningPeriod**函数将使用类型为 Time 的维度的默认级别和成员。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函数类似于**OpeningPeriod**函数，不同之处在于**ClosingPeriod**函数返回最后一个同级，而不是第一个同级。  
  
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
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
