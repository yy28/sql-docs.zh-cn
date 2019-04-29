---
title: 处理 Analysis Services 对象 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1cd8be08afc7ea0e8e7bf811db4e26208a2feae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930920"
---
# <a name="processing-analysis-services-objects"></a>处理 Analysis Services 对象
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  处理影响下列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象类型： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、多维数据集、维度、度量值组、分区、数据挖掘结构和模型。 对于每个对象，可以指定对象的处理级别，也可以指定“处理默认值”选项以允许 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动选择最优的处理级别。 有关每个对象的不同处理等级的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 应注意处理行为的后果以减少负面影响。 例如，完全处理某个维度会将所有依赖于此维度的分区自动设置为未处理状态。 这将使受影响的多维数据集在依赖分区得到处理之前变得无法查询。  
  
 本主题包含以下各节：  
  
 [处理数据库](#bkmk_procdb)  
  
 [处理维度](#bkmk_procdim)  
  
 [处理多维数据集](#bkmk_proccube)  
  
 [处理度量值组](#bkmk_procmeasure)  
  
 [处理分区](#bkmk_procpartition)  
  
 [处理数据挖掘结构和模型](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> 处理数据库  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，数据库包含的是对象而不是数据。 处理数据库时，您指挥服务器以递归方式处理在模型中存储数据的那些对象，例如维度、分区、挖掘结构和挖掘模型。  
  
 处理数据库时，还会一并处理数据库包含的某些或全部分区、维度和挖掘模型。 实际的处理类型随每个对象的状态和所选处理选项的不同而不同。 有关详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
##  <a name="bkmk_proccube"></a> 处理多维数据集  
 可将多维数据集认为是度量值组和分区的包装对象。 多维数据集除一个或多个度量值之外，还包括维度，都存储在分区中。 维度定义了数据在多维数据集中的分布方式。 在处理多维数据集时，会发出一个 SQL 查询检索事实数据表，以便使用相应的度量值填充多维数据集中的每个成员。 对于多维数据集中指向节点的任意特定路径，都存在一个值或一个可计算的值。  
  
 处理多维数据集时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 处理多维数据集中任何未处理的维度和多维数据集中度量值组内的部分或所有分区。 这些细节取决于处理开始时对象的状态及所选的处理选项。 有关处理选项的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 处理多维数据集将创建存储相关事实数据的、可用计算机处理的文件。 如果创建了聚合，则这些聚合存储在聚合数据文件中。 然后，就可以从 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的对象资源管理器或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> 处理维度  
 处理维度时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 依照维度表编写和运行查询以返回处理所需的信息。  
  
|Country|销售区域|State|  
|-------------|------------------|-----------|  
|United States|West|California|  
|United States|West|Oregon|  
|United States|West|Washington|  
  
 处理操作本身可将表格格式数据转换为可用的层次结构。 这些层次结构使用非常清楚的成员名称，内部采用唯一的数字路径表示。 以下示例是层次结构的一个文本表示形式。  
  
||  
|-|  
|[United States]|  
|[United States].[West]|  
|[United States].[West].[California]|  
|[United States].[West].[Oregon]|  
|[United States].[West].[Washington]|  
  
 维度处理不能创建或更新在多维数据集级别定义的计算成员。 更新多维数据集定义时会影响计算成员。 而且，维度处理不会创建或更新聚合。 但是，维度处理会导致聚合被删除。 只有在处理分区期间才能创建或更新聚合。  
  
 处理某个维度时，应该明白该维度可能用于好几个多维数据集中。 处理该维度时，这些多维数据集被标记为未处理并且变得无法查询。 若要同时处理维度及相关的多维数据集，请使用批处理设置。 有关详细信息，请参阅 [批处理 (Analysis Services)](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)。  
  
##  <a name="bkmk_procmeasure"></a> 处理度量值组  
 处理某个度量值组时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会一并处理该度量值组内的某些或全部分区和所有参与该度量值组的未处理维度。 处理作业的细节取决于所选择的处理选项。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，您可以处理一个或多个度量值组而不影响多维数据集中的其他度量值组。  
  
> [!NOTE]  
>  可以通过编程方式或使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]处理各个度量值组。 不能在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中处理各个度量值组；但是可以按分区进行处理。  
  
##  <a name="bkmk_procpartition"></a> 处理分区  
 有效的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理涉及到数据的分区操作。 分区处理十分特别，因为它需要考虑硬盘使用和空间约束，以及 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]施加的数据结构限制。 若要保持较快的查询响应时间以及较高的处理吞吐量，必须定期创建、处理和合并分区。 合并分区期间，认识到可能会集成冗余数据这一情况并对此进行管理非常重要。 有关详细信息，请参阅[在 Analysis Services 中合并分区（SSAS - 多维）](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)。  
  
 处理某个分区时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将根据所选择的处理选项来处理该分区和其中存在的所有未处理维度。 使用分区为处理提供了以下几种好处。 可以处理某个分区而不影响多维数据集中的其他分区。 存储受单元写回影响的数据时，分区非常有用。 写回是一项功能，它使得用户能够通过将新数据写入分区并查看预计更改的效果来执行假设分析。 如果要使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的单元写回功能，则需要有一个写回分区。 以并行方式处理分区非常有用，因为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 能够更有效地利用处理能力，并可显著缩短总处理时间。 您还可以按顺序处理分区。  
  
##  <a name="bkmk_procdm"></a> 处理数据挖掘结构和模型  
 挖掘结构定义了数据挖掘模型将据以生成的数据域。 一个挖掘结构可以包含多个挖掘模型。 可以将挖掘结构和与其关联的挖掘模型分开处理。 单独处理挖掘结构时，将使用数据源的定型数据对其进行填充。  
  
 处理数据挖掘模型时，将定型数据传递给挖掘模型算法，使用数据挖掘算法为模型定型，然后生成内容。 有关数据挖掘模型对象的详细信息，请参阅[挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 有关处理挖掘结构和模型的详细信息，请参阅[处理要求和注意事项（数据挖掘）](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 [用于处理的工具和方法 (Analysis Services)](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [批处理 (Analysis Services)](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
