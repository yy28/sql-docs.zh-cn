---
title: 设计聚合 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81450789395dfef84f81896990fa251514d3489e
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156129"
---
# <a name="designing-aggregations-xmla"></a>设计聚合 (XMLA)
  聚合设计与特定度量值组的分区相关联，以确保分区在存储聚合时使用相同的结构。 对分区使用相同的存储结构可让你可以轻松地定义可使用更高版本合并的分区[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令。 有关聚合设计的详细信息，请参阅[聚合和聚合设计](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
 若要定义的聚合设计的聚合，可以使用[DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla)命令 XML for Analysis (XMLA) 中。 `DesignAggregations` 命令拥有一些属性，这些属性可标识要用作引用的聚合设计以及如何基于该引用控制设计过程。 使用 `DesignAggregations` 命令及其属性，可以采用迭代方式设计聚合或成批设计聚合，并可查看生成的设计统计信息，以评估设计过程。  
  
## <a name="specifying-an-aggregation-design"></a>指定聚合设计  
 [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性的`DesignAggregations`命令必须包含对现有聚合设计的对象引用。 该对象引用包含数据库标识符、多维数据集标识符、度量值组标识符和聚合设计标识符。 如果该聚合设计不存在，则会出现错误。  
  
## <a name="controlling-the-design-process"></a>控制设计过程  
 您可以使用 `DesignAggregations` 命令的下列属性控制用于为聚合设计定义聚合的算法：  
  
-   [步骤](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla)属性确定多少次迭代`DesignAggregations`控制权返还给客户端应用程序之前，应该执行命令。  
  
-   [时间](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla)属性确定的毫秒数`DesignAggregations`控制权返还给客户端应用程序之前，应该执行命令。  
  
-   [优化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla)属性确定的性能提高百分比估计的值`DesignAggregations`命令应尝试获得。 如果要以迭代方式设计聚合，只需在第一条命令中发送此属性。  
  
-   [存储](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla)属性确定估计的磁盘存储，以字节为单位，由`DesignAggregations`命令。 如果要以迭代方式设计聚合，只需在第一条命令中发送此属性。  
  
-   [具体化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla)属性确定是否`DesignAggregations`命令应创建在设计过程中定义的聚合。 如果要以迭代方式设计聚合，则应在准备好保存所设计的聚合之前，将此属性设置为 false。 如果设置为 true，则当前设计过程将会终止，并会将所定义的聚合添加到指定的聚合设计中。  
  
## <a name="specifying-queries"></a>指定查询  
 DesignAggregations 命令通过包含一个或多个支持基于使用情况的优化命令`Query`中的元素[查询](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla)属性。 `Queries`属性可以包含一个或多个[查询](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)元素。 如果 `Queries` 属性不包含任何 `Query` 元素，则 `Object` 元素中指定的聚合设计将使用包含一组常规聚合的默认结构。 设计此组常规聚合的目的是为了满足 `Optimization` 命令的 `Storage` 和 `DesignAggregations` 属性中指定的条件。  
  
 每个 `Query` 元素表示一个目标查询，设计进程使用这些查询定义以最常用的查询为目标的聚合。 您可以指定自己的目标查询，也可以使用查询日志中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例存储的信息来检索最常用查询的相关信息。 基于使用情况的优化向导会在发送 `DesignAggregations` 命令时，基于时间、使用情况或指定的用户，使用查询日志来检索目标查询。 有关详细信息，请参阅[基于使用情况的优化向导的 F1 帮助](../usage-based-optimization-wizard-f1-help.md)。  
  
 如果您迭代式地设计聚合，则只需要在第一个 `DesignAggregations` 命令中传递目标查询，这是因为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例存储这些目标查询，并在执行后续 `DesignAggregations` 命令时使用这些查询。 在迭代进程的第一个`DesignAggregations` 命令中传递目标查询后，任何在 `DesignAggregations` 属性中包含目标查询的后续 `Queries` 命令都会生成错误。  
  
 `Query` 元素包含一个以逗号分隔的值，该值包含以下参数：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *频率*  
 与该查询此前执行的次数对应的加权系数。 如果`Query`元素表示一个新查询，*频率*值表示设计进程用于评估该查询的加权系数。 在设计进程中，随着频率值变大，该查询的权重也会增加。  
  
 *数据集*  
 一个数字字符串，该字符串指定维度中的哪些属性要包括在该查询中。 此字符串的字符个数必须与维度中的属性个数相同。 零 (0) 指示指定序号位置的属性不包括在指定维度的查询中，而 1 指示指定序号位置的属性包括在指定维度的查询中。  
  
 例如，字符串“011”所指的查询涉及具有三个属性的维度，其中第二个和第三个属性包括在该查询中。  
  
> [!NOTE]  
>  某些属性与数据集无关。 有关排除的属性的详细信息，请参阅[查询元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)。  
  
 包含聚合设计的度量值组中每个维度都由*数据集*中的值`Query`元素。 *Dataset* 值的顺序必须与包括在度量值组中的维度的顺序一致。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>使用迭代过程或批处理过程设计聚合  
 您可以根据设计过程所要求的交互性，将 `DesignAggregations` 命令用作迭代过程或批处理过程的一部分。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>使用迭代过程设计聚合  
 若要以迭代方式设计聚合，请发送多个 `DesignAggregations` 命令，以精确地控制设计过程。 聚合设计向导使用同样的方法精确控制设计过程。 有关详细信息，请参阅[聚合设计向导 F1 帮助](../aggregation-design-wizard-f1-help.md)。  
  
> [!NOTE]  
>  以迭代方式设计聚合需要显式会话。 有关显式会话的详细信息，请参阅[管理连接和会话&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)。  
  
 若要开始迭代过程，先要发送一条包含以下信息的 `DesignAggregations` 命令：  
  
-   整个设计过程的目标 `Storage` 和 `Optimization` 属性值。  
  
-   对设计过程的第一步进行限制的 `Steps` 和 `Time` 属性值。  
  
-   如果希望进行基于使用情况的优化，则还要提供包含作为整个设计过程目标的目标查询的 `Queries` 属性。  
  
-   设置为 false 的 `Materialize` 属性。 将此属性设置为 false 指示当命令完成时，设计过程不会将所定义的聚合保存到聚合设计中。  
  
 当第一条 `DesignAggregations` 命令执行完毕后，它会返回一个包含设计统计信息的行集。 您可以对这些设计统计信息进行评估，以确定设计过程是应继续还是已完成。 如果设计过程应继续，则应发送另一条 `DesignAggregations` 命令，其中包含对此步设计过程进行限制的 `Steps` 和 `Time` 值。 您要对结果统计信息进行评估，然后确定设计过程是否应继续。 这种发送 `DesignAggregations` 命令并对结果进行评估的迭代过程将一直继续下去，直至达到目标并定义了一组适当的聚合为止。  
  
 得到一组您需要的聚合后，应发送最后一条 `DesignAggregations` 命令。 最后一条 `DesignAggregations` 命令的 `Steps` 属性应设置为 1，`Materialize` 属性应设置为 true。 通过这些设置，此最后一条 `DesignAggregations` 命令将结束设计过程，并将所设计的聚合保存到聚合设计中。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>使用批处理过程设计聚合  
 您还可以发送包含作为整个设计过程目标和对整个设计过程进行限制的 `DesignAggregations`、`Steps`、`Time` 和 `Storage` 属性的单条 `Optimization` 命令，从而以批处理方式设计聚合。 如果希望进行基于使用情况的优化，则 `Queries` 属性中还应包含作为整个设计过程目标的目标查询。 此外，请确保将 `Materialize` 属性设置为 true，以使命令执行完毕时，设计过程会将所设计的聚合保存到聚合设计中。  
  
 您可以在隐式或显式会话中使用批处理过程来设计聚合。 有关隐式和显式会话的详细信息，请参阅[管理连接和会话&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)。  
  
## <a name="returning-design-statistics"></a>返回设计统计信息  
 当 `DesignAggregations` 命令将控制权返还给客户端应用程序之后，该命令会返回一个包含一行的行集，该行包含命令的设计统计信息。 下表列出了该行集包含的列。  
  
|“列”|数据类型|Description|  
|------------|---------------|-----------------|  
|步骤|Integer|在将控制权返还给客户端应用程序之前，命令执行的步数。|  
|Time|Long integer|在将控制权返还给客户端应用程序之前，命令运行的毫秒数。|  
|Optimization|双精度|在将控制权返还给客户端应用程序之前，命令获得的性能提高百分比估计值。|  
|存储|Long integer|在将控制权返还给客户端应用程序之前，命令占用的存储空间的估计字节数。|  
|Aggregations|Long integer|在将控制权返还给客户端应用程序之前，命令定义的聚合数。|  
|LastStep|Boolean|指示行集中的数据是否表示设计过程的最后一步。 如果命令的 `Materialize` 属性设置为 true，则此列的值设置为 true。|  
  
 在迭代和批处理设计过程中，您都可以使用每个 `DesignAggregations` 命令执行完毕之后所返回的行集中包含的设计统计信息。 在迭代设计过程中，您可以使用设计统计信息来确定并显示进度。 以批处理方式设计聚合时，您可以使用设计统计信息来确定命令所创建的聚合数。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
