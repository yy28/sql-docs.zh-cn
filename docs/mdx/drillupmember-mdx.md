---
title: DrillupMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5dfdec16d20173639cc92a80b1ca546f44b70334
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049188"
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)


  返回指定集中不是第二个指定集中成员的后代的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **DrillupMember**函数将返回一组基于指定第一个集中的第二个集中成员的后代的成员的成员。 第一个集可以具有任何维数，但第二个集必须包含一个一维集。 第一个集中的原始成员顺序会被保留。 此函数在构造集时仅包括位于第一个集中并且是第二个集中成员的直接后代的那些成员。 如果第一个集中某成员的直接祖先不在第二个集中，则第一个集中的该成员包括在此函数返回的集中。 第一个集中位于第二个集中某个祖先成员之前的后代，也会包括在内。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
> [!IMPORTANT]  
>  只有后面紧跟子成员或后代的成员才会被浅化。 在集中的成员的顺序非常重要的这两种向下钻取\*和向上钻取\*系列的函数。 请考虑使用**Hierarchize**函数进行正确排序的第一组的成员。  
  
## <a name="example"></a>示例  
 除了第二个集以外，以下三个示例都是相似的。 在第一个示例时，第二个集为 United States。 因此，从结果集中排除 Colorado。 它是 United States 的后代。  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 示例二向我们显示了成员顺序的重要性。 由于**DrillupMember**仅浅化紧跟第一个集中的后代的那些成员，它不浅化 Canada 成员。 Canada 与其后代由 United States 和 Colorado 分隔开来。 如果你对成员重新排序，使 Canada 直接位于 Alberta 上方，则 Alberta 和 Brunswick 都将从行集中排除。  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 示例三显示了如何使用**Hierarchize**可以降低成员顺序和浅化 Canada 成员的效果。  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
