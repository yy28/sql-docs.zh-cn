---
title: "设计聚合 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fdc973309fe87792aa135813c23e4e68d7650043
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="designing-aggregations-xmla"></a>设计聚合 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]聚合设计都要确保分区存储聚合时使用相同的结构的特定度量值组分区与关联。 为分区使用相同的存储结构可让你轻松地定义可以使用更高版本合并的分区[MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)命令。 有关聚合设计的详细信息，请参阅[聚合和聚合设计](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
 若要定义的聚合设计的聚合，可以使用[DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) XML Analysis (XMLA) 命令。 **DesignAggregations**命令具有标识要用作引用以及如何控制基于该引用的设计过程的聚合设计的属性。 使用**DesignAggregations**命令并将其属性，您可以以迭代方式或批处理中，设计聚合，然后查看生成的设计统计信息来评估设计过程。  
  
## <a name="specifying-an-aggregation-design"></a>指定聚合设计  
 [对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)属性**DesignAggregations**命令必须包含对的现有聚合设计的对象引用。 该对象引用包含数据库标识符、多维数据集标识符、度量值组标识符和聚合设计标识符。 如果该聚合设计不存在，则会出现错误。  
  
## <a name="controlling-the-design-process"></a>控制设计过程  
 你可以使用的以下属性**DesignAggregations**命令来控制用于定义聚合的聚合设计的算法：  
  
-   [步骤](../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md)属性确定的迭代数**DesignAggregations**之前它将控制权返回到客户端应用程序，应该执行命令。  
  
-   [时间](../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)属性确定的毫秒数**DesignAggregations**之前它将控制权返回到客户端应用程序，应该执行命令。  
  
-   [优化](../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md)属性确定的性能改善的估计的百分比**DesignAggregations**命令应尝试实现。 如果要以迭代方式设计聚合，只需在第一条命令中发送此属性。  
  
-   [存储](../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md)属性确定磁盘存储，以字节为单位，使用的估计的量**DesignAggregations**命令。 如果要以迭代方式设计聚合，只需在第一条命令中发送此属性。  
  
-   [Materialize](../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md)属性确定是否**DesignAggregations**命令应创建设计过程中定义的聚合。 如果要以迭代方式设计聚合，则应在准备好保存所设计的聚合之前，将此属性设置为 false。 如果设置为 true，则当前设计过程将会终止，并会将所定义的聚合添加到指定的聚合设计中。  
  
## <a name="specifying-queries"></a>指定的查询  
 DesignAggregations 命令通过包括一个或多个支持基于使用情况的优化命令**查询**中的元素[查询](../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)属性。 **查询**属性可以包含一个或多个[查询](../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md)元素。 如果**查询**属性不包含任何**查询**中指定的元素，聚合设计**对象**元素使用包含的默认结构聚合常规集。 聚合此常规组旨在满足中指定的条件**优化**和**存储**属性**DesignAggregations**命令。  
  
 每个 **Query** 元素表示一个目标查询，设计进程使用这些查询定义以最常用的查询为目标的聚合。 你可以指定您自己的目标查询，也可以使用存储的实例的信息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在要检索信息是最常用的查询日志中使用查询。 基于使用情况的优化向导使用查询日志来检索基于时间、 使用情况或指定的用户，在发送时的目标查询**DesignAggregations**命令。 有关详细信息，请参阅[基于使用情况的优化向导的 F1 帮助](http://msdn.microsoft.com/library/e5f5a938-ae7c-4f4e-9416-a7f94ac82763)。  
  
 以迭代方式设计聚合，如果你只需在第一个传递目标查询**DesignAggregations**命令因为[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例将存储这些目标查询，并在后续期间使用这些查询**DesignAggregations**命令。 在迭代进程的第一个 **DesignAggregations** 命令中传递目标查询后，任何在 **DesignAggregations** 属性中包含目标查询的后续 **Queries** 命令都会生成错误。  
  
 **Query** 元素包含一个以逗号分隔的值，该值包含以下参数：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *频率*  
 与该查询此前执行的次数对应的加权系数。 如果 **Query** 元素表示一个新查询，则 *Frequency* 值表示设计进程用于评估该查询的加权系数。 在设计进程中，随着频率值变大，该查询的权重也会增加。  
  
 *数据集*  
 一个数字字符串，该字符串指定维度中的哪些属性要包括在该查询中。 此字符串的字符个数必须与维度中的属性个数相同。 零 (0) 指示指定序号位置的属性不包括在指定维度的查询中，而 1 指示指定序号位置的属性包括在指定维度的查询中。  
  
 例如，字符串“011”所指的查询涉及具有三个属性的维度，其中第二个和第三个属性包括在该查询中。  
  
> [!NOTE]  
>  某些属性与数据集无关。 有关排除特性的详细信息，请参阅[查询元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md).  
  
 包含聚合设计的度量值组中的每个维度都由 *Query* 元素中的 **Dataset** 值表示。 *Dataset* 值的顺序必须与包括在度量值组中的维度的顺序一致。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>使用迭代过程或批处理过程设计聚合  
 你可以使用**DesignAggregations**的迭代过程或批处理，具体取决于所需的设计过程的交互性的一部分的命令。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>使用迭代过程设计聚合  
 若要以迭代方式设计聚合，你将发送多个**DesignAggregations**命令提供很好的控制设计过程。 聚合设计向导使用同样的方法精确控制设计过程。 有关详细信息，请参阅[聚合设计向导 F1 帮助](http://msdn.microsoft.com/library/39e23cf1-6405-4fb6-bc14-ba103314362d)。  
  
> [!NOTE]  
>  以迭代方式设计聚合需要显式会话。 有关显式会话的详细信息，请参阅[管理连接和会话 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
 若要启动的迭代过程，第一次发送**DesignAggregations**命令包含以下信息：  
  
-   **存储**和**优化**上为目标的整个设计过程的属性值。  
  
-   **步骤**和**时间**在其设计过程的第一步是有限的属性值。  
  
-   如果你想基于使用情况的优化**查询**属性包含目标查询上为目标的整个设计过程。  
  
-   **Materialize**属性设置为 false。 将此属性设置为 false 指示当命令完成时，设计过程不会将所定义的聚合保存到聚合设计中。  
  
 当第一个**DesignAggregations**命令运行完以后，该命令将返回包含设计统计信息的行集。 您可以对这些设计统计信息进行评估，以确定设计过程是应继续还是已完成。 如果应继续该过程，你之后要发送另一个**DesignAggregations**命令包含**步骤**和**时间**与其设计的此步骤中处理的值受到限制。 您要对结果统计信息进行评估，然后确定设计过程是否应继续。 发送此迭代过程**DesignAggregations**命令和评估的结果继续，直到达到你的目标和具有相应的一组定义的聚合。  
  
 你已达到所需的聚合集后，你将发送最后一个**DesignAggregations**命令。 此最终**DesignAggregations**命令应具有其**步骤**属性设置为 1 并且其**Materialize**属性设置为 true。 通过使用这些设置，这最终**DesignAggregations**命令完成设计过程，并将定义的聚合保存到的聚合设计。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>使用批处理过程设计聚合  
 你还可以在批处理中的聚合设计通过发送单个**DesignAggregations**命令包含**步骤**，**时间**，**存储**，和**优化**属性值为目标并局限整个设计过程。 如果你想基于使用情况的优化，在设计过程的目标在其的目标查询，还应在包括**查询**属性。 此外请确保**Materialize**属性被设置为 true，因此设计过程将定义的聚合保存到的聚合设计时在该命令完成。  
  
 您可以在隐式或显式会话中使用批处理过程来设计聚合。 有关隐式和显式会话的详细信息，请参阅[管理连接和会话 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
## <a name="returning-design-statistics"></a>返回设计统计信息  
 当**DesignAggregations**命令将控件返回到客户端应用程序，该命令将返回包含表示命令的设计统计信息的单个行的行集。 下表列出了该行集包含的列。  
  
|“列”|数据类型|Description|  
|------------|---------------|-----------------|  
|步骤|Integer|在将控制权返还给客户端应用程序之前，命令执行的步数。|  
|Time|Long integer|在将控制权返还给客户端应用程序之前，命令运行的毫秒数。|  
|Optimization|双精度|在将控制权返还给客户端应用程序之前，命令获得的性能提高百分比估计值。|  
|存储器|Long integer|在将控制权返还给客户端应用程序之前，命令占用的存储空间的估计字节数。|  
|Aggregations|Long integer|在将控制权返还给客户端应用程序之前，命令定义的聚合数。|  
|LastStep|Boolean|指示行集中的数据是否表示设计过程的最后一步。 如果**Materialize**命令的属性设置为此列的值设置为 true，则为 true。|  
  
 你可以使用包含在返回每一个之后的行集的设计统计信息**DesignAggregations**迭代中的命令和批处理设计。 在迭代设计过程中，您可以使用设计统计信息来确定并显示进度。 以批处理方式设计聚合时，您可以使用设计统计信息来确定命令所创建的聚合数。  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
