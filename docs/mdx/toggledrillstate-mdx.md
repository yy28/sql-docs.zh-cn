---
title: ToggleDrillState (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bcd09f9c7ea8be177112e2a70ef04380ebc00146
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582379"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *递归*  
 （可选）。 指示集的递归比较的关键字。 **ToggleDrillState**技术支持部门的组合**DrillupMember**和**DrilldownMember**函数。 成员是中时，才应用递归**DrilldownMember**状态。  
  
 *Include_calc_members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>Remarks  
 **ToggleDrillState**函数切换位于第一个集中的第二个集的每个成员的钻取状态。 第一个集可以包含任意维数的元组，但是第二个集必须包含单个维度的成员。 **ToggleDrillState**技术支持部门的组合**DrillupMember**和**DrilldownMember**函数。 如果该成员， *m*，第二个集是否位于第一个集，以及该成员向下钻取 （即，具有紧靠它的后代），然后`DrillupMember(Set_Expression1, {m})`应用于成员或元组中的第一个集。 如果该*m*向上钻成员 (即，没有任何子代*m*紧跟*m*)，`DrilldownMember(Set_Expression1, {m}[, RECURSIVE])`应用于第一个组。  
  
 如果可选**递归**标记用于、 向上钻取和向下的钻取以递归方式应用。 有关递归标志的详细信息，请参阅[DrillupMember](../mdx/drillupmember-mdx.md)和[DrilldownMember](../mdx/drilldownmember-mdx.md)函数。  
  
 查询的 XMLA 属性 MdpropMdxDrillFunctions，您可以验证服务器提供钻函数; 支持的级别请参阅[支持 XMLA 属性&#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)有关详细信息。  
  
 请参阅[数据库日志： MDX Set 函数： ToggleDrillState() 函数](http://go.microsoft.com/fwlink/?LinkId=517759)有关方案和示例涉及此函数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
