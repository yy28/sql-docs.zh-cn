---
title: DrilldownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ab4ee77bad08ab3883645ad5e2628a265aa4e9
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144892"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  深化第一个指定集与第二个指定集的交集中的成员。  
  
 该函数也可以通过使用第一个元组层次结构或者可选的指定层次结构，对一组元组进行深化。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *Target_Hierarchy*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *递归*  
 指示集的递归比较的关键字。  
  
 *Include_Calc_Members*  
 用于使计算成员能够包括在深化结果中的关键字。  
  
## <a name="remarks"></a>备注  
 该函数返回按层次结构排序的子成员集，并包括第一个集和第二个集的交集中的成员。 如果第一个集包含父成员以及一个或多个子成员，则不深化父成员。 第一个集可以具有任何维数，但第二个集必须包含一个一维集。 第一个集中的原始成员的顺序将保留，只不过该函数的结果集中包含的所有子成员都紧随在它们的父成员之后。 该函数将通过检索第一个集与第二个集的交集中的每个成员的子成员来构造结果集。 如果**递归**指定，则该函数的后续结果集内的成员与第二个集，检索结果集直到没有更多还存在第二个集中的每个成员的子级进行递归比较从结果集中的成员可以在第二个集中找到。  
  
 查询 XMLA 属性**MdpropMdxDrillFunctions**使您可以验证服务器为钻取功能提供支持的级别; 请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
 第一个集可以包含元组，但不能包含成员。 对元组的深化是一种 OLE DB 扩展，这种深化将返回元组集而非成员集。  
  
> [!IMPORTANT]  
>  当成员后面紧跟其子成员之一时，将不会深化该成员。 在集中的成员的顺序非常重要的向下钻取 * 和 Drillup\*系列的函数。  
  
## <a name="examples"></a>示例  
 下例深化了 Australia 成员，它是第一个集与第二个集的交集成员。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下例深化了 Australia 成员，它是第一个集与第二个集的交集成员。 但是，由于指定了 RECURSIVE 参数，该函数会继续将结果集的成员（State-Province 级别的成员）与第二个集中的成员进行递归比较，检索结果集（City 级别的成员）与第二个集的交集中的每个成员的子成员，直到找遍结果集与第二个集的交集中的成员为止。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
