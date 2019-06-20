---
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58acac77e4826855997791476b0602699452b7b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228081"
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
  
 *递归*  
 （可选）。 指示集的递归比较的关键字。 **ToggleDrillState**函数是一系列**DrillupMember**并**DrilldownMember**函数。 当成员处于时才适用递归**DrilldownMember**状态。  
  
 *Include_calc_members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>备注  
 **ToggleDrillState**函数切换是存在于第一个集中的第二个集的每个成员的钻取状态。 第一个集可以包含任意维数的元组，但是第二个集必须包含单个维度的成员。 **ToggleDrillState**函数是一系列**DrillupMember**并**DrilldownMember**函数。 如果该成员*m*，第二个集是存在于第一个集中，该成员被深化 （即，有一个后代紧跟它），然后`DrillupMember(Set_Expression1, {m})`应用于第一个集中的元组的成员。 如果该*m*成员被浅 (即，没有任何子代*m*中紧跟*m*)，`DrilldownMember(Set_Expression1, {m}[, RECURSIVE])`应用于第一个集。  
  
 如果可选**递归**使用标志，向上钻取和向下的钻取以递归方式应用。 关于循环标志的详细信息，请参阅[DrillupMember](../mdx/drillupmember-mdx.md)并[DrilldownMember](../mdx/drilldownmember-mdx.md)函数。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
 请参阅[数据库日志：MDX 集函数：Toggledrillstate （） 函数](https://go.microsoft.com/fwlink/?LinkId=517759)的方案和示例涉及此函数。  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
