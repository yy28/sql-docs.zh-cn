---
title: "AMO 数据挖掘类 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4eeb92697ce1a6a8475fa973a51ee6bdf9536b0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="amo-data-mining-classes"></a>AMO 数据挖掘类
  数据挖掘类可帮助您创建、修改、删除和处理数据挖掘对象。 处理数据挖掘对象包括创建数据挖掘结构、创建数据挖掘模型以及处理这些模型。  
  
 有关如何设置环境，和有关的详细信息<xref:Microsoft.AnalysisServices.Server>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>，和<xref:Microsoft.AnalysisServices.DataSourceView>对象，请参阅[AMO 基础类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)。  
  
 定义分析管理对象 (AMO) 中的对象需要设置每个对象的多个属性以设置正确的上下文。 复杂对象（例如 OLAP 和数据挖掘对象）需要较长且详细的编码。  
  
 本主题包含以下各节：  
  
-   [MiningStructure 对象](#MiningStructure)  
  
-   [MiningModel 对象](#MiningModel)  
  
 下图显示了本主题中介绍的类之间的关系。  
  
 ![AMO 数据挖掘类](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-dataminingclasses.gif "AMO 数据挖掘类")  
  
##  <a name="MiningStructure"></a>MiningStructure 对象  
 挖掘结构是挖掘模型的容器。 该结构定义了挖掘模型可使用的所有可能列。 每个挖掘模型都在该挖掘结构的已定义列集中定义自己的列。  
  
 简单的 <xref:Microsoft.AnalysisServices.MiningStructure> 对象包括基本信息、数据源视图、一个或多个 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>、零个或多个 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 以及 <xref:Microsoft.AnalysisServices.MiningModelCollection>。  
  
 基本信息包括 <xref:Microsoft.AnalysisServices.MiningStructure> 对象的名称和 ID（内部标识符）。  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 对象包含挖掘结构的基础数据模型。  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 是具有单个值的列或属性。  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 是具有每个事例的多个值的列或属性。  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection> 包含根据同一数据生成的所有挖掘模型。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 对象是通过以下方式创建的：将其添加到数据库的 <xref:Microsoft.AnalysisServices.MiningStructureCollection>，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.MiningStructure> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.MiningStructure> 对象，必须使用 <xref:Microsoft.AnalysisServices.MiningStructure> 对象的 Drop 方法来删除。 从集合中删除 <xref:Microsoft.AnalysisServices.MiningStructure> 对象不会影响服务器。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 可使用它自己的处理方法进行处理，也可在父对象使用自己的处理方法进行自身处理时进行处理。  
  
### <a name="columns"></a>列  
 列包含模型的数据，根据用法不同可为不同类型：Key、Input、Predictable 或 InputPredictable。 可预测列是生成挖掘模型的目标。  
  
 单值列在 AMO 中称为 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。 多值列称为 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 简单的 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 对象由基本信息、类型、内容和数据绑定组成。  
  
 基本信息包括 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 的名称和 ID（内部标识符）。  
  
 类型是指值的数据类型：LONG、BOOLEAN、TEXT、DOUBLE、DATE。  
  
 内容告知引擎如何对列进行建模。 值可以为：Discrete、Continuous、Discretized、Ordered、Cyclical、Probability、Variance、StdDev、ProbabilityVariance、ProbabilityStdDev、Support 和 Key。  
  
 数据绑定通过数据源视图元素将数据挖掘列链接到基础数据模型。  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 是通过以下方式创建的：将其添加到父 <xref:Microsoft.AnalysisServices.MiningStructureCollection>，然后使用 Update 方法将父 <xref:Microsoft.AnalysisServices.MiningStructure> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>，则必须从父 <xref:Microsoft.AnalysisServices.MiningStructure> 集合中将其删除，然后必须使用 Update 方法将父 <xref:Microsoft.AnalysisServices.MiningStructure> 对象更新到服务器中。  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 简单的 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 对象由基本信息和标量列组成。  
  
 基本信息包括 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 的名称和 ID（内部标识符）。  
  
 标量列为 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 是通过以下方式创建的：将其添加到父 <xref:Microsoft.AnalysisServices.MiningStructure> 集合，然后使用 Update 方法将父 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>，必须从父 <xref:Microsoft.AnalysisServices.MiningStructure> 集合中将其删除，然后必须使用 Update 方法将父 <xref:Microsoft.AnalysisServices.MiningStructure> 对象更新到服务器中。  
  
##  <a name="MiningModel"></a>MiningModel 对象  
 <xref:Microsoft.AnalysisServices.MiningModel> 对象可用于选择要使用结构中的哪些列、要使用的算法以及用于优化模型的可选特定参数。 例如，您可能想要在同一个挖掘结构中定义使用相同算法的多个挖掘模型，但要在一个模型中忽略挖掘结构的某些列，而在另一个模型中将这些列用作输入，在第三个模型中将这些列用作输入和预测。 当在一个挖掘模型中要将某列视为连续列，而在另一个模型中您要将该列视为离散化列时，此对象非常有用。  
  
 简单的 <xref:Microsoft.AnalysisServices.MiningModel> 对象由基本信息、算法定义和列组成。  
  
 基本信息包括挖掘模型的名称和 ID（内部标识符）。  
  
 算法定义是指 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中提供的任一标准算法，或服务器上启用的任何自定义算法。  
  
 列是算法及其用法定义所用列的集合。  
  
 <xref:Microsoft.AnalysisServices.MiningModel> 是通过以下方式创建的：将其添加到数据库的 <xref:Microsoft.AnalysisServices.MiningModelCollection>，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.MiningModel> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.MiningModel>，则必须使用 <xref:Microsoft.AnalysisServices.MiningModel> 的 Drop 方法来删除。 从集合中删除 <xref:Microsoft.AnalysisServices.MiningModel> 不会影响服务器。  
  
 创建 <xref:Microsoft.AnalysisServices.MiningModel> 后，便可使用它自己的处理方法进行处理，也可在父对象使用自己的处理方法进行自身处理时进行处理。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [AMO 基础类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [编程 AMO 数据挖掘对象](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-data-mining-objects.md)   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [逻辑体系结构 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

