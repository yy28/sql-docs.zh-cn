---
description: Properties (MDX)
title: " (MDX) 的属性 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbdae47b3ede8ad2b22258e83a69b4f2776115d9
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192337"
---
# <a name="properties-mdx"></a>Properties (MDX)


  返回一个包含成员属性值的字符串，或返回一个强类型值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Property_Name*  
 成员属性名称的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 **Properties**函数返回指定成员属性的指定成员的值。 成员属性可以是任何内部成员属性，如 **NAME**、 **ID**、 **KEY**或 **CAPTION**，也可以是用户定义的成员属性。 有关详细信息，请参阅 [&#40;mdx&#41;的内部成员属性 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 和 [用户定义的成员属性 &#40;mdx&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)。  
  
 默认情况下，将该值强迫为一个字符串。 如果指定了 **类型化** ，则返回值为强类型。  
  
-   如果属性是内部的，则函数返回成员的原始类型。  
  
-   如果属性类型是用户定义的，则返回值的类型与 **MemberValue** 函数的返回值的类型相同。  
  
> [!NOTE]  
>  Properties ('Key') 返回与 Key0 相同的结果，但组合键除外。 Properties ('Key') 将为组合键返回 null。 将 Key*x* 语法用于组合键，如示例中所示。 Properties('Key0')、Properties('Key1')、Properties('Key2') 等共同构成了组合键。  
  
## <a name="example"></a>示例  
 下例既返回内部属性也返回用户定义成员属性，并且利用 TYPED 参数返回“星期几”成员属性的强类型值。  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例演示 KEY*x* 属性的用法。  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;MDX&#41;使用成员属性 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
