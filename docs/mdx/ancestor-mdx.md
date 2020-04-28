---
title: 祖先（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 385206d4a94362831e0949bafe5a11c1ce48d7bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017136"
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)


  此函数返回指定成员在指定级别或距离处的祖先。  
  
## <a name="syntax"></a>语法  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *距离*  
 指定与指定成员距离的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 使用**上级**函数时，您可以为函数提供一个 mdx 成员表达式，然后提供一个级别的 mdx 表达式，该表达式是成员的上级，或是表示该成员以上的级别数的数值表达式。 利用此信息，**上级**函数返回该级别的祖先成员。  
  
> [!NOTE]  
>  若要返回包含祖先成员的集，而不只是祖先成员，请使用[&#40;MDX&#41;](../mdx/ancestors-mdx.md)函数的上级。  
  
 如果指定了级别表达式，则**上级**函数返回指定成员在指定级别上的祖先。 如果指定成员与指定级别不在同一个层次结构中，该函数将返回错误。  
  
 如果指定了距离，则**上级**函数返回指定成员的祖先，该成员是在成员表达式指定的层次结构中指定的步骤数。 可以将成员指定为属性层次结构的成员或用户定义层次结构的成员，有时还可以指定为父子层次结构的成员。 数值 1 返回成员的父成员，数值 2 返回成员的祖父成员（如果存在）。 数值 0 返回成员本身。  
  
> [!NOTE]  
>  对于父级别未知或无法命名的情况，请使用此窗体的**上级**函数。  
  
## <a name="examples"></a>示例  
 下面的示例使用一个级别表达式，并返回 Australia 中每个 State-Province 的 Internet Sales Amount 及其占 Australia 总 Internet Sales Amount 的百分比。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用一个数值表达式，并返回 Australia 中每个 State-Province 的 Internet Sales Amount 及其占所有国家总 Internet Sales Amount 的百分比。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
