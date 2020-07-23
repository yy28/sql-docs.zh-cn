---
title: ToggleDrillState （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ffe8cb97ffa8dd01b058d5cf71fc2f0922e11501
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971475"
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
 （可选）。 指示集的递归比较的关键字。 **ToggleDrillState**函数是**DrillupMember**和**DrilldownMember**函数的组合。 仅当成员处于**DrilldownMember**状态时，递归才适用。  
  
 *Include_calc_members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>备注  
 **ToggleDrillState**函数用于切换第一个集中出现的第二个集的每个成员的钻取状态。 第一个集可以包含任意维数的元组，但是第二个集必须包含单个维度的成员。 **ToggleDrillState**函数是**DrillupMember**和**DrilldownMember**函数的组合。 如果第二个集的成员*m*位于第一个集中，并且该成员被向下钻取（即，在其后面紧跟一个后代），则 `DrillupMember(Set_Expression1, {m})` 将应用于第一个集中的成员或元组。 如果已向上钻取该*m*成员（即，没有*m 的后代* *），* `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 则应用于第一个集。  
  
 如果使用了可选的**递归**标志，则将以递归方式应用向上钻取和向下钻取。 有关递归标志的详细信息，请参阅[DrillupMember](../mdx/drillupmember-mdx.md)和[DrilldownMember](../mdx/drilldownmember-mdx.md)函数。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅[&#40;xmla&#41;支持的 Xmla 属性](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)。  
  
 请参阅[数据库日志： MDX 集函数：适用于方案的 ToggleDrillState （）函数](https://go.microsoft.com/fwlink/?LinkId=517759)和涉及此函数的示例。  
  
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
  
  
