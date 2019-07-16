---
title: 属性 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7d6e072cd47233b6cb76c09fb3bc0e9b9b42604
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020648"
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
 **属性**函数将返回指定的成员属性的指定成员的值。 成员属性可以是任何内部成员属性，如**名称**， **ID**，**密钥**，或者**标题**，也可以是用户定义的成员属性。 有关详细信息，请参阅[内部成员属性&#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)并[用户定义成员属性&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
 默认情况下，将该值强迫为一个字符串。 如果**类型化**指定，则返回值强类型。  
  
-   如果属性是内部的，则函数返回成员的原始类型。  
  
-   如果属性类型是用户定义，返回值的类型是返回值的类型相同**MemberValue**函数。  
  
> [!NOTE]  
>  Properties ('Key') 返回与 Key0 相同的结果，但组合键除外。 Properties ('Key') 将为组合键返回 null。 使用键*x*语法用于组合键，如示例所示。 Properties('Key0')、Properties('Key1')、Properties('Key2') 等共同构成了组合键。  
  
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
  
 下面的示例演示使用密钥*x*属性。  
  
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
  
## <a name="see-also"></a>请参阅  
 [使用成员属性 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
