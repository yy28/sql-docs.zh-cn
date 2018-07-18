---
title: 离散化方法 （数据挖掘） |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 610108ce4edb6e3beb5c13398d0a79eca200bdba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016974"
---
# <a name="discretization-methods-data-mining"></a>离散化方法（数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中创建数据挖掘模型时使用的某些算法需要特定的内容类型才能正常运行。 例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 算法的输入不能为连续列，并且不能预测连续值。 另外，有些列可能会因包含的值太多而导致算法不易标识数据中据以创建模型的相关模式。  
  
 在这些情况下，可以将列中的数据离散化，以便能够使用算法来生成挖掘模型。 “离散化 ”是将值放入存储桶中以便得到有限数目的可能状态的过程。 存储桶本身是作为有序且离散的值处理的。 数值列和字符串列都可以进行离散化。  
  
 离散化数据时，可以使用多种方法。 如果数据挖掘解决方案使用关系数据，则通过设置 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 属性的值可以控制对数据分组所使用的存储桶数。 默认存储桶数为 5。  
  
 如果数据挖掘解决方案使用联机分析处理 (OLAP) 多维数据集中的数据，数据挖掘算法将使用以下公式自动计算要生成的存储桶数，其中 n 是列中数据非重复值的数目：  
  
 `Number of Buckets = sqrt(n)`  
  
 如果不希望由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 计算存储桶数目，则可使用 <xref:Microsoft.AnalysisServices.DimensionAttribute.DiscretizationBucketCount%2A> 属性来手动指定存储桶的数目。  
  
 下表说明了可在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中用于离散化数据的方法。  
  
|离散化方法|Description|  
|---------------------------|-----------------|  
|**AUTOMATIC**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 确定要使用的离散化方法。|  
|**群集**|该算法可以对定型数据采样，初始化为一些随机点，然后使用 Expectation Maximization (EM) 聚类分析方法运行几次 Microsoft 聚类分析算法迭代，以此将数据分组。 由于 **CLUSTERS** 方法可用于所有分布曲线，所以该方法很有用。 但是，该方法所需的处理时间比其他离散化方法的处理时间长。<br /><br /> 此方法只能用于数值列。|  
|**EQUAL_AREAS**|该算法将数据分成值数目相同的若干个组。 此方法最适用于正常分布曲线，但如果分布包含的值数量很大，并且这些值在连续数据的窄组中，则此方法的使用效果不是很好。 例如，如果项有一半的成本为 0，那么这一半数据将位于曲线上的某个点以下。 在这种分布中，此方法将对数据进行分解，以便在多个区域中建立相同的离散化。 这样一来，生成的数据表示形式就会不准确。|  
  
## <a name="remarks"></a>注释  
  
-   可以使用 **EQUAL_AREAS** 方法来离散化字符串。  
  
-   **CLUSTERS** 方法使用 1000 个随机记录样本来离散化数据。 如果不希望算法对数据采样，请使用 **EQUAL_AREAS** 方法。  
  
  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [内容类型 & #40; DMX & #41;](../../dmx/content-types-dmx.md)   
 [数据挖掘算法 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘结构 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [数据类型 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [挖掘结构列](../../analysis-services/data-mining/mining-structure-columns.md)   
 [列分布（数据挖掘）](../../analysis-services/data-mining/column-distributions-data-mining.md)  
  
  
