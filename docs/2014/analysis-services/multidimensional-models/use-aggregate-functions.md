---
title: 使用聚合函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68ec0250382ad6ec865ff37adcb847ba6afec978
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257543"
---
# <a name="use-aggregate-functions"></a>使用聚合函数
  使用维度来切分度量值时，按该维度中包含的层次结构汇总该度量值。 汇总行为取决于为度量值指定的聚合函数。 对于包含数字数据的度量值，聚合函数是 `Sum`。 度量值的值的总和将根据活动的层次结构的级别而异。  
  
 在 Analysis Services 中，你创建的每一个度量值均由确定该度量值的操作的聚合函数备份。 预定义的聚合类型包括`Sum`， `Min`， `Max`， `Count`，**非重复计数**，以及多个其他更专用的函数。 或者，如果需要基于复杂或自定义公式的聚合，可以生成 MDX 计算，而非使用预生成的聚合函数。 例如，如果想定义一个百分比值的度量值，你将在 MDX 中使用计算度量值执行该操作。 请参阅 [CREATE MEMBER 语句 (MDX)](/sql/mdx/mdx-data-definition-create-member)。  
  
 对通过“多维数据集向导”创建的度量值分配了作为度量值定义的一部分的聚合类型。 聚合类型始终是`Sum`，假设源列包含数字数据。 `Sum` 分配而不考虑源列的数据类型。 例如，如果你使用“多维数据集向导”创建度量值并从事实数据表中拉入所有列，则你将注意到所有所得度量值均具有 `Sum` 的聚合，即使源是日期时间列。 始终检查通过向导创建的度量值的预分配的聚合方法，以确保聚合函数恰当。  
  
 可在多维数据集定义之一中分配或更改聚合方法，方式为通过 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]，或通过 MDX。 有关详细说明，请参阅[在多维模型中创建度量值和度量值组](create-measures-and-measure-groups-in-multidimensional-models.md)或[聚合 (MDX)](/sql/mdx/aggregate-mdx)。  
  
##  <a name="AggFunction"></a> 聚合函数  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 提供了几种函数，用来针对包含在度量值组中的维度聚合度量值。 聚合函数的 *累加性* 可确定度量值如何在多维数据集的所有维度中进行聚合。 聚合函数具有三个级别的累加性：  
  
 累加性  
 累加性度量值也称为完全累加性度量值，可针对包含度量值的度量值组中包括的所有维度进行聚合，没有任何限制。  
  
 半累加性  
 半累加性度量值可针对包含度量值的度量值组中包括的某些（但不是全部）维度进行聚合。 例如，表示可供库存数量的度量值可针对地域维度进行聚合，以生成可用于所有仓库的总计数量，但该度量值不能针对时间维度进行聚合，因为该度量值表示可用数量的定期快照。 针对时间维度聚合此类度量值将产生不正确的结果。 有关详细信息，请参阅 [Define Semiadditive Behavior](define-semiadditive-behavior.md) 。  
  
 非累加性  
 非累加性度量值不能针对包含度量值的度量值组中的任何维度进行聚合。 相反，必须对表示度量值的多维数据集中的每个单元分别计算度量值。 例如，返回百分比的计算度量值（例如利润率）不能由任何维度内子成员的百分比值进行聚合。  
  
 下表列出了 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的聚合函数，并对函数的累加性和预期输出进行了说明。  
  
|聚合函数|累加性|返回值|  
|--------------------------|----------------|--------------------|  
|`Sum`|累加性|对所有子成员的值求和。 这是默认的聚合函数。|  
|`Count`|累加性|检索所有子成员的计数。|  
|`Min`|半累加性|检索所有子成员的最低值。|  
|`Max`|半累加性|检索所有子成员的最高值。|  
|`DistinctCount`|非累加性|检索所有唯一子成员的计数。 有关详细信息，请参阅下一节中的 [About Distinct Count Measures](use-aggregate-functions.md#bkmk_distinct) 。|  
|`None`|非累加性|不执行任何聚合，直接从事实数据表中为包含度量值的度量值组提供维度中叶成员和非叶成员的所有值。 如果从事实数据表中无法为成员读取任何值，则该成员的值设置为空。|  
|`ByAccount`|半累加性|根据为帐户维度中某一成员的帐户类型指定的聚合函数计算聚合。 如果度量值组中不存在任何帐户类型维度，视为`None`聚合函数。<br /><br /> 有关帐户维度的详细信息，请参阅 [创建父子类型维度的财务帐户](database-dimensions-finance-account-of-parent-child-type.md)。|  
|`AverageOfChildren`|半累加性|计算所有非空子成员的平均值。|  
|`FirstChild`|半累加性|检索第一个子成员的值。|  
|`LastChild`|半累加性|检索最后一个子成员的值。|  
|`FirstNonEmpty`|半累加性|检索第一个非空子成员的值。|  
|`LastNonEmpty`|半累加性|检索最后一个非空子成员的值。|  
  
##  <a name="bkmk_distinct"></a> About Distinct Count Measures  
 “聚合函数”  属性值为 **Distinct Count** 的度量值称为非重复计数度量值。 非重复计数度量值可以用于对维度的最低级别成员在事实数据表中的出现次数进行计数。 由于计数具有非重复性，因此，如果某个成员出现多次，则仅对此成员进行一次计数。 非重复计数度量值始终位于专用的度量值组中。 将非重复计数度量值放入其自己的度量值组是内置到设计器中作为性能优化技术的最佳做法。  
  
 非重复计数度量值通常用于确定对于某个维度的每个成员，另一维度有多少不同的最低级别成员共享事实数据表中的。 例如，在“销售额”多维数据集中，对于每个客户和客户组，购买了多少不同的产品？ （即，对于“客户”维度的每个成员，“产品”维度有多少不同的最低级别成员共享事实数据表中的行？）或者，例如在“Internet 站点访问”多维数据集中，对于每个站点访问者和站点访问者组，访问了 Internet 站点上有多少不同的页？ （即，对于“站点访问者”维度的每个成员，“页”维度有多少不同的最低级别成员共享事实数据表中的行？）在上述每个示例中，第二个维度的最低级别成员由非重复计数度量值进行计数。  
  
 此类分析无需限制为两个维度。 事实上，非重复计数度量值可以由多维数据集中的任何维度组合进行分隔和切片，这些维度组合包括具有计数成员的维度。  
  
 对成员进行计数的非重复计数度量值基于事实数据表中的外键列。 （即，度量值的“源列”属性标识此列。）此列联接标识由非重复计数度量值进行计数的成员的维度表列。  
  
## <a name="see-also"></a>请参阅  
 [度量值和度量值组](measures-and-measure-groups.md)   
 [MDX 函数引用&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [定义半累加性行为](define-semiadditive-behavior.md)  
  
  
