---
title: "MDX 函数引用 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- member functions [MDX]
- level functions [MDX]
- MDX [Analysis Services], functions
- array functions
- string functions
- Multidimensional Expressions [Analysis Services], functions
- hierarchy functions [MDX]
- numeric functions [MDX]
- tuple functions
- subcube functions [MDX]
- functions [MDX]
- logical functions [MDX]
- set functions [MDX]
ms.assetid: e363722a-3e5b-40a9-a0b5-399dd2d93f6d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c9e43eacb0fe9b5c5af98cfe54b557af93af7d1c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-function-reference-mdx"></a>MDX 函数参考 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]多维表达式 (MDX) 语法中的函数使用提供了。 函数可以在任何有效的 MDX 语句中使用，并且经常用于查询、自定义汇总定义以及其他计算。 本节介绍 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 附带的 MDX 函数。  
  
 可以使用下面这些表按返回值的类别来查找函数，也可以从按字母顺序排列的目录中按名称来选择函数。  
  
## <a name="array-functions"></a>数组函数  
  
|函数|Description|  
|--------------|-----------------|  
|[SetToArray &#40;MDX &#41;](../mdx/settoarray-mdx.md)|将一个或多个集转换为数组，以便在用户定义函数中使用。|  
  
## <a name="hierarchy-functions"></a>层次结构函数  
  
|函数|Description|  
|--------------|-----------------|  
|[层次结构 &#40;MDX &#41;](../mdx/hierarchy-mdx.md)|返回包含指定的成员或级别的层次结构。|  
|[维度 &#40;MDX &#41;](../mdx/dimension-mdx.md)|返回包含指定的成员、级别或层次结构的维度。|  
|[维度 &#40;MDX &#41;](../mdx/dimensions-mdx.md)|返回由数值表达式或字符串表达式指定的层次结构。|  
  
## <a name="level-functions"></a>级别函数  
  
|函数|Description|  
|--------------|-----------------|  
|[级别 &#40;MDX &#41;](../mdx/level-mdx.md)|返回成员的级别。|  
|[级别 &#40;MDX &#41;](../mdx/levels-mdx.md)|返回由数值表达式指定在维度或层次结构中的位置的级别，或返回由字符串表达式指定名称的级别。|  
  
## <a name="logical-functions"></a>逻辑函数  
  
|函数|Description|  
|--------------|-----------------|  
|[IsAncestor &#40;MDX &#41;](../mdx/isancestor-mdx.md)|返回一个指定成员是否为另一个指定成员的祖先。|  
|[IsEmpty &#40;MDX &#41;](../mdx/isempty-mdx.md)|返回表达式的计算结果是否为空单元值。|  
|[IsGeneration &#40;MDX &#41;](../mdx/isgeneration-mdx.md)|返回指定成员是否处于指定的代中。|  
|[IsLeaf &#40;MDX &#41;](../mdx/isleaf-mdx.md)|返回指定成员是否为叶成员。|  
|[IsSibling &#40;MDX &#41;](../mdx/issibling-mdx.md)|返回一个指定成员是否为另一个指定成员的同级成员。|  
  
## <a name="member-functions"></a>成员函数  
  
|函数|Description|  
|--------------|-----------------|  
|[上级 &#40;MDX &#41;](../mdx/ancestor-mdx.md)|返回某个成员在指定级别或距离上的祖先。|  
|[ClosingPeriod &#40;MDX &#41;](../mdx/closingperiod-mdx.md)|返回某个成员在指定级别上的后代中的最后一个同级。|  
|[Cousin &#40;MDX &#41;](../mdx/cousin-mdx.md)|返回与指定的子成员在父成员下方具有相同的相对位置的子成员。|  
|[CurrentMember &#40;MDX &#41;](../mdx/currentmember-mdx.md)|返回迭代过程中指定的维度或层次结构的当前成员。|  
|[DataMember &#40;MDX &#41;](../mdx/datamember-mdx.md)|返回系统生成的、与某个维度的非叶成员相关联的数据成员。|  
|[DefaultMember &#40;MDX &#41;](../mdx/defaultmember-mdx.md)|返回维度或层次结构的默认成员。|  
|[FirstChild &#40;MDX &#41;](../mdx/firstchild-mdx.md)|返回成员的第一个子成员。|  
|[FirstSibling &#40;MDX &#41;](../mdx/firstsibling-mdx.md)|返回成员的父成员的第一个子成员。|  
|[项 &#40;成员 &#41;&#40;MDX &#41;](../mdx/item-member-mdx.md)|返回指定元组中的成员。|  
|[Lag &#40;MDX &#41;](../mdx/lag-mdx.md)|返回在所在维度中位置比指定成员靠前且靠前位数为指定位数的成员。|  
|[LastChild &#40;MDX &#41;](../mdx/lastchild-mdx.md)|返回指定成员的最后一个子成员。|  
|[LastSibling &#40;MDX &#41;](../mdx/lastsibling-mdx.md)|返回指定成员的父成员的最后一个子成员。|  
|[主管 &#40;MDX &#41;](../mdx/lead-mdx.md)|返回在所在维度中位置比指定成员靠后且靠后位数为指定位数的成员。|  
|[LinkMember &#40;MDX &#41;](../mdx/linkmember-mdx.md)|返回相当于指定层次结构中的指定成员的成员。|  
|[成员 &#40;字符串 &#41;&#40;MDX &#41;](../mdx/members-string-mdx.md)|返回字符串表达式所指定的成员。|  
|[NextMember &#40;MDX &#41;](../mdx/nextmember-mdx.md)|返回指定成员所在级别的下一个成员。|  
|[OpeningPeriod &#40;MDX &#41;](../mdx/openingperiod-mdx.md)|返回指定级别（也可以是指定成员）的后代中的第一个同级。|  
|[ParallelPeriod &#40;MDX &#41;](../mdx/parallelperiod-mdx.md)|返回上一期间中与指定成员具有相同的相对位置的成员。|  
|[父 &#40;MDX &#41;](../mdx/parent-mdx.md)|返回成员的父成员。|  
|[PrevMember &#40;MDX &#41;](../mdx/prevmember-mdx.md)|返回指定成员所在级别的上一个成员。|  
|[StrToMember &#40;MDX &#41;](../mdx/strtomember-mdx.md)|返回由 MDX 格式的字符串指定的成员。|  
|[UnknownMember &#40;MDX &#41;](../mdx/unknownmember-mdx.md)|返回与级别或成员相关联的未知成员。|  
|[ValidMeasure &#40;MDX &#41;](../mdx/validmeasure-mdx.md)|通过将不适用的维度强制到其顶层，来返回虚拟多维数据集中的有效度量值。|  
  
## <a name="numeric-functions"></a>数值函数  
  
|函数|Description|  
|--------------|-----------------|  
|[聚合 &#40;MDX &#41;](../mdx/aggregate-mdx.md)|返回一个标量值，该标量值由对指定集的元组的度量值聚合而得，或通过使用指定的数值表达式对指定集的元组计算而得（可选）。|  
|[Avg &#40;MDX &#41;](../mdx/avg-mdx.md)|返回对所指定集计算所得的度量值的平均值，或可选数值表达式对所指定集求得的平均值。|  
|[CalculationCurrentPass (MDX)](../mdx/calculationcurrentpass-mdx.md)|针对指定的查询上下文返回多维数据集的当前计算传递。|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|返回用 MDX 表达式对多维数据集的指定的计算传递求得的值。|  
|[CoalesceEmpty &#40;MDX &#41;](../mdx/coalesceempty-mdx.md)|将空单元值合并成数字或字符串并返回合并后的值。|  
|[相关 &#40;MDX &#41;](../mdx/correlation-mdx.md)|返回对集求值的两个序列的相关系数。|  
|[计数 &#40; 维度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)|返回多维数据集中的维度数。|  
|[计数 &#40;层次结构级别 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)|返回维度或层次结构中的级别数。|  
|[计数 &#40;集 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)|返回集中的单元数。|  
|[计数 &#40;元组 &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)|返回元组中的维度数。|  
|[协变 &#40;MDX &#41;](../mdx/covariance-mdx.md)|返回两个序列用有偏差总体公式对集求得的总体协方差。|  
|[CovarianceN &#40;MDX &#41;](../mdx/covariancen-mdx.md)|返回两个序列用无偏差总体公式对集求得的样本协方差。|  
|[DistinctCount &#40;MDX &#41;](../mdx/distinctcount-mdx.md)|返回集中非重复的非空元组的数目。|  
|[IIf &#40;MDX &#41;](../mdx/iif-mdx.md)|返回由逻辑测试确定的两个值之一。|  
|[LinRegIntercept &#40;MDX &#41;](../mdx/linregintercept-mdx.md)|一组线性回归计算，并返回回归线中的截距的值 y = ax + b。|  
|[LinRegPoint &#40;MDX &#41;](../mdx/linregpoint-mdx.md)|一组线性回归计算，并返回的值*y*在回归行中，y = ax + b。|  
|[LinRegR2 &#40;MDX &#41;](../mdx/linregr2-mdx.md)|对集进行线性回归计算，并返回确定系数 R2。|  
|[LinRegSlope &#40;MDX &#41;](../mdx/linregslope-mdx.md)|一组中，线性回归计算，并在回归行中，返回的值的斜率 y = ax + b。|  
|[LinRegVariance &#40;MDX &#41;](../mdx/linregvariance-mdx.md)|一组中，线性回归计算，并返回与回归线，关联的方差 y = ax + b。|  
|[LookupCube &#40;MDX &#41;](../mdx/lookupcube-mdx.md)|返回用 MDX 表达式对同一数据库中另一个指定的多维数据集求得的值。|  
|[最大 &#40;MDX &#41;](../mdx/max-mdx.md)|返回对集求值的数值表达式的最大值。|  
|[中值 &#40;MDX &#41;](../mdx/median-mdx.md)|返回对集求值的数值表达式的中值。|  
|[最小值 &#40;MDX &#41;](../mdx/min-mdx.md)|返回对集求值的数值表达式的最小值。|  
|[序号 &#40;MDX &#41;](../mdx/ordinal-mdx.md)|返回与某一级别相关联的从零开始计算的序数值。|  
|[预测 &#40;MDX &#41;](../mdx/predict-mdx.md)|返回用数值表达式对数据挖掘模型求得的值。|  
|[级别 &#40;MDX &#41;](../mdx/rank-mdx.md)|返回指定元组在指定集中的排名（从 1 开始）。|  
|[RollupChildren &#40;MDX &#41;](../mdx/rollupchildren-mdx.md)|使用指定的一元运算符，通过汇总指定成员的子成员的值，从而返回所生成的值。|  
|[Stddev &#40;MDX &#41;](../mdx/stddev-mdx.md)|别名[Stdev &#40;MDX &#41;](../mdx/stdev-mdx.md).|  
|[总体标准偏差 &#40;MDX &#41;](../mdx/stddevp-mdx.md)|别名[StdevP &#40;MDX &#41;](../mdx/stdevp-mdx.md).|  
|[Stdev &#40;MDX &#41;](../mdx/stdev-mdx.md)|返回数值表达式用无偏差总体公式对集求得的样本标准偏差。|  
|[StdevP &#40;MDX &#41;](../mdx/stdevp-mdx.md)|返回数值表达式用有偏差总体公式对集求得的总体标准偏差。|  
|[StrToValue &#40;MDX &#41;](../mdx/strtovalue-mdx.md)|返回由 MDX 格式的字符串指定的值。|  
|[Sum &#40;MDX &#41;](../mdx/sum-mdx.md)|返回用数值表达式对集求得的值之和。|  
|[值 &#40;MDX &#41;](../mdx/value-mdx.md)|返回度量值的值。|  
|[Var &#40;MDX &#41;](../mdx/var-mdx.md)|返回数值表达式用无偏差总体公式对集求得的样本方差。|  
|[方差 &#40;MDX &#41;](../mdx/variance-mdx.md)|别名[Var &#40;MDX &#41;](../mdx/var-mdx.md).|  
|[VarianceP &#40;MDX &#41;](../mdx/variancep-mdx.md)|别名[VarP &#40;MDX &#41;](../mdx/varp-mdx.md).|  
|[VarP &#40;MDX &#41;](../mdx/varp-mdx.md)|返回数值表达式用有偏差总体公式对集求得的总体方差。|  
  
## <a name="set-functions"></a>集函数  
  
|函数|Description|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40;MDX &#41;](../mdx/addcalculatedmembers-mdx.md)|返回通过将计算成员添加到指定集而生成的集。|  
|[AllMembers &#40;MDX &#41;](../mdx/allmembers-mdx.md)|返回包含所指定维度、层次结构或级别的所有成员（包括计算成员）的集。|  
|[上级 &#40;MDX &#41;](../mdx/ancestors-mdx.md)|返回由成员的指定级别或距离的所有祖先构成的集。|  
|[祖先 &#40;MDX &#41;](../mdx/ascendants-mdx.md)|返回指定成员的祖先集（包含该成员本身）。|  
|[轴 &#40;MDX &#41;](../mdx/axis-mdx.md)|返回轴中定义的集。|  
|[BottomCount &#40;MDX &#41;](../mdx/bottomcount-mdx.md)|按升序对集进行排序，并返回指定数目的最小值元组。|  
|[BottomPercent &#40;MDX &#41;](../mdx/bottompercent-mdx.md)|按升序对集进行排序，并返回一个最小值元组集，该元组集的累积合计等于或小于指定的百分比。|  
|[BottomSum &#40;MDX &#41;](../mdx/bottomsum-mdx.md)|按升序对集进行排序，并返回一个最小值元组集，该元组集的合计等于或小于指定值。|  
|[子级 &#40;MDX &#41;](../mdx/children-mdx.md)|返回指定成员的子级。|  
|[叉积 &#40;MDX &#41;](../mdx/crossjoin-mdx.md)|返回一个或多个集的叉积。|  
|[CurrentOrdinal &#40;MDX &#41;](../mdx/currentordinal-mdx.md)|返回迭代过程中集内的当前迭代数。|  
|[后代 &#40;MDX &#41;](../mdx/descendants-mdx.md)|返回成员在指定级别或距离上的后代集，可以选择包括或不包括其他级别的后代。|  
|[非重复 &#40;MDX &#41;](../mdx/distinct-mdx.md)|返回从指定集中删除了重复元组后得到的集。|  
|[DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)|将某个集的成员深化到该集中所表示的最低级别的下一级，或者深化到该集中所表示的某一任意指定的成员级别的下一级。|  
|[DrilldownLevelBottom &#40;MDX &#41;](../mdx/drilldownlevelbottom-mdx.md)|将集中某一指定级别上的最底层成员深化到下一个级别。|  
|[DrilldownLevelTop &#40;MDX &#41;](../mdx/drilldownleveltop-mdx.md)|将集中某一指定级别上最顶端的成员深化到下一个级别。|  
|[DrilldownMember &#40;MDX &#41;](../mdx/drilldownmember-mdx.md)|深化第一个指定集与第二个指定集的交集中的成员。 另外，该函数可对元组集进行深化。|  
|[DrilldownMemberBottom &#40;MDX &#41;](../mdx/drilldownmemberbottom-mdx.md)|深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 另外，此函数也可对元组集进行深化。|  
|[DrilldownMemberTop &#40;MDX &#41;](../mdx/drilldownmembertop-mdx.md)|深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 另外，此函数可对元组集进行深化。|  
|[DrillupLevel &#40;MDX &#41;](../mdx/drilluplevel-mdx.md)|浅化某个集在指定级别以下的成员。|  
|[DrillupMember &#40;MDX &#41;](../mdx/drillupmember-mdx.md)|浅化第一个指定集和第二个指定集的交集的成员。|  
|[除 &#40;MDX &#41;](../mdx/except-mdx-function.md)|查找两个集之间不同的项，可以选择保留重复项。|  
|[存在 &#40;MDX &#41;](../mdx/exists-mdx.md)|返回一个集的一组成员，该组成员与一个或多个其他集的一个或多个元组共存。|  
|[提取 &#40;MDX &#41;](../mdx/extract-mdx.md)|返回由提取的维度元素中的元组构成的集。|  
|[筛选器 &#40;MDX &#41;](../mdx/filter-mdx.md)|返回根据搜索条件对指定集进行筛选后得到的集。|  
|[生成 &#40;MDX &#41;](../mdx/generate-mdx.md)|将一个集应用于另一个集中的每个成员，然后对得到的集求并集。 另外，此函数返回通过用字符串表达式对集求值而创建的串联字符串。|  
|[Head &#40;MDX &#41;](../mdx/head-mdx.md)|返回集中指定数目的前几个元素，同时保留重复项。|  
|[Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)|对层次结构中的某个集的成员进行排序。|  
|[相交 &#40;MDX &#41;](../mdx/intersect-mdx.md)|返回两个输入集的交集，可以选择保留重复项。|  
|[LastPeriods &#40;MDX &#41;](../mdx/lastperiods-mdx.md)|返回指定成员之前（包含该成员）的成员集。|  
|[成员 &#40;集 &#41;&#40;MDX &#41;](../mdx/members-set-mdx.md)|返回某个维度、级别或层次结构中的成员集。|  
|[Mtd &#40;MDX &#41;](../mdx/mtd-mdx.md)|按照时间维度中的年级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。|  
|[NameToSet &#40;MDX &#41;](../mdx/nametoset-mdx.md)|返回由 MDX 格式的字符串指定的成员组成的集。|  
|[NonEmptyCrossjoin &#40;MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)|以集的形式返回一个或多个集的叉积，不包括空元组和没有关联事实数据表数据的元组。|  
|[顺序 &#40;MDX &#41;](../mdx/order-mdx.md)|排列指定集的成员，可以选择保留或打乱原有的层次结构。|  
|[PeriodsToDate &#40;MDX &#41;](../mdx/periodstodate-mdx.md)|按照时间维度中的指定级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。|  
|[Qtd &#40;MDX &#41;](../mdx/qtd-mdx.md)|为给定成员，与第一个同级的开始和结束与约束通过将给定成员属于同一级别返回一组同级成员*季度*时间维度中的级别。|  
|[同级 &#40;MDX &#41;](../mdx/siblings-mdx.md)|返回指定成员的同级，包括该成员本身。|  
|[StripCalculatedMembers &#40;MDX &#41;](../mdx/stripcalculatedmembers-mdx.md)|返回通过从指定的集中删除计算成员而生成的集。|  
|[StrToSet &#40;MDX &#41;](../mdx/strtoset-mdx.md)|返回由 MDX 格式的字符串指定的集。|  
|[子集 &#40;MDX &#41;](../mdx/subset-mdx.md)|返回指定集中元组的子集。|  
|[结尾 &#40;MDX &#41;](../mdx/tail-mdx.md)|返回集末尾的子集。|  
|[ToggleDrillState &#40;MDX &#41;](../mdx/toggledrillstate-mdx.md)|切换成员的钻取状态。|  
|[TopCount &#40;MDX &#41;](../mdx/topcount-mdx.md)|按降序对集进行排序，并返回指定数目的最大值元素。|  
|[TopPercent &#40;MDX &#41;](../mdx/toppercent-mdx.md)|按降序对集进行排序，并返回一个最大值元组集，该元组集的累积合计等于或小于指定的百分比。|  
|[TopSum &#40;MDX &#41;](../mdx/topsum-mdx.md)|对集进行排序并返回累计合计至少达到指定值的最前面的元素。|  
|[联合 &#40;MDX &#41;](../mdx/union-mdx.md)|返回两个集的并集，可以选择保留重复项。|  
|[Unorder &#40;MDX &#41;](../mdx/unorder-mdx.md)|从指定集中删除任何强制排序。|  
|[VisualTotals &#40;MDX &#41;](../mdx/visualtotals-mdx.md)|返回通过动态计算指定集内子成员的合计而生成的集，可以选择在得到的单元集内对父成员名称应用某种模式。|  
|[Wtd &#40;MDX &#41;](../mdx/wtd-mdx.md)|按照时间维度中的周级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。|  
|[Ytd &#40;MDX &#41;](../mdx/ytd-mdx.md)|为给定成员，与第一个同级的开始和结束与约束通过将给定成员属于同一级别返回一组同级成员*年*时间维度中的级别。|  
  
## <a name="string-functions"></a>字符串函数  
  
|函数|Description|  
|--------------|-----------------|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|返回用 MDX 表达式对多维数据集的指定计算传递求得的值。|  
|[CoalesceEmpty &#40;MDX &#41;](../mdx/coalesceempty-mdx.md)|将空单元值合并成数字或字符串并返回合并后的值。|  
|[生成 &#40;MDX &#41;](../mdx/generate-mdx.md)|将一个集应用于另一个集中的每个成员，然后对得到的集求并集。 另外，此函数返回通过用字符串表达式对集求值而创建的串联字符串。|  
|[IIf &#40;MDX &#41;](../mdx/iif-mdx.md)|返回由逻辑测试确定的两个值之一。|  
|[LookupCube &#40;MDX &#41;](../mdx/lookupcube-mdx.md)|返回用 MDX 表达式对同一数据库中另一个指定的多维数据集求得的值。|  
|[MemberToStr &#40;MDX &#41;](../mdx/membertostr-mdx.md)|返回与指定成员对应的 MDX 格式的字符串。|  
|[名称 &#40;MDX &#41;](../mdx/name-mdx.md)|返回维度、层次结构、级别或成员的名称。|  
|[属性 &#40;MDX &#41;](../mdx/properties-mdx.md)|返回一个包含成员属性值的字符串，或返回一个强类型值。|  
|[SetToStr &#40;MDX &#41;](../mdx/settostr-mdx.md)|返回与指定集对应的 MDX 格式的字符串。|  
|[TupleToStr &#40;MDX &#41;](../mdx/tupletostr-mdx.md)|返回与指定元组对应的 MDX 格式的字符串。|  
|[UniqueName &#40;MDX &#41;](../mdx/uniquename-mdx.md)|返回指定的维度、层次结构、级别或成员的唯一名称。|  
|[用户名 &#40;MDX &#41;](../mdx/username-mdx.md)|返回当前连接的域名和用户名。|  
  
## <a name="subcube-functions"></a>子多维数据集函数  
  
|函数|Description|  
|--------------|-----------------|  
|[这 &#40;MDX &#41;](../mdx/this-mdx.md)|返回当前的子多维数据集。|  
|[使 &#40;MDX &#41;](../mdx/leaves-mdx.md)|返回指定维度、成员或元组中的叶成员集。|  
  
## <a name="tuple-functions"></a>元组函数  
  
|函数|Description|  
|--------------|-----------------|  
|[当前 &#40;MDX &#41;](../mdx/current-mdx.md)|返回迭代过程中集内的当前元组。|  
|[项 &#40;元组 &#41;&#40;MDX &#41;](../mdx/item-tuple-mdx.md)|返回某个集中的元组。|  
|[根 &#40;MDX &#41;](../mdx/root-mdx.md)|返回组成的元组**所有**多维数据集、 维度或元组中每个属性层次结构中的成员。|  
|[StrToTuple &#40;MDX &#41;](../mdx/strtotuple-mdx.md)|返回由 MDX 格式的字符串指定的元组。|  
  
## <a name="other-functions"></a>其他函数  
  
|函数|Description|  
|--------------|-----------------|  
|[错误 &#40;MDX &#41;](../mdx/error-mdx.md)|引发错误，根据需要可以选择提供指定的错误消息。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 &#40;MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
