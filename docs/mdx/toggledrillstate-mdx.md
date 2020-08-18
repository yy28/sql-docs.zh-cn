---
description: ToggleDrillState (MDX)
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e10c62742e28b69545efac51f70bf9628b43e08d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412891"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  在成员之间切换深化模式和浅化模式的状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *Recursive*  
 （可选）。 指示集的递归比较的关键字。 **ToggleDrillState**函数是**DrillupMember**和**DrilldownMember**函数的组合。 仅当成员处于 **DrilldownMember** 状态时，递归才适用。  
  
 *Include_calc_members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>备注  
 **ToggleDrillState**函数用于切换第一个集中出现的第二个集的每个成员的钻取状态。 第一个集可以包含任意维数的元组，但是第二个集必须包含单个维度的成员。 **ToggleDrillState**函数是**DrillupMember**和**DrilldownMember**函数的组合。 如果第二个集的成员 *m*位于第一个集中，并且该成员被深化 (即，在其后面紧跟有后代) ，则 `DrillupMember(Set_Expression1, {m})` 将其应用于第一个集中的成员或元组。 如果对该*m*成员进行钻取 (即，则不会在*m) 紧*挨着的*m*的后代， `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 应用于第一个集。  
  
 如果使用了可选的 **递归** 标志，则将以递归方式应用向上钻取和向下钻取。 有关递归标志的详细信息，请参阅 [DrillupMember](../mdx/drillupmember-mdx.md) 和 [DrilldownMember](../mdx/drilldownmember-mdx.md) 函数。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅 [&#40;xmla&#41;支持的 Xmla 属性 ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
 有关涉及此函数的方案和示例，请参阅 [数据库日志： MDX 集函数： ToggleDrillState ( # A1 函数](https://go.microsoft.com/fwlink/?LinkId=517759) 。  
  
## <a name="example"></a>示例  
 下例对第一个集中的澳大利亚成员进行深化，而对第一个集中的美国成员进行浅化。  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
