---
title: 了解通过 1103年表格对象模型在级别 1050年 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77e602c40567fb36cbca8a9d441635711328c82b
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="understanding-tabular-object-model-at-levels-1050-through-1103"></a>在通过 1103年级别 1050年了解表格对象模型
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]

  表格模型是表、关系、层次结构、透视、度量值和关键绩效的逻辑表示形式。 本节介绍使用 AMO 的内部实现。 请参阅[使用分析管理对象开发&#40;AMO&#41; ](../../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)如果你尚未使用之前的 AMO。  
  
 此处的方法是自上而下的，表格模型中的所有相关对象逻辑上映射到 AMO 对象，并说明所需的交互或工作流。 可以从 Codeplex 获得一个源的代码示例，用于创建表格模型使用 AMO，AMO 到表格示例。 请注意，示例中的代码仅作为对此处所述逻辑概念的支持提供，不应用于生产环境中。 不提供对示例的支持或保修。  
  
## <a name="database-representation"></a>数据库表示形式  
 数据库为表格模型提供容器对象。 表格模型中的所有对象包含在数据库中。 就 AMO 对象而言，数据库表示形式与 `xref:Microsoft.AnalysisServices.Database` 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在建模时使用。  
  
 请参阅[数据库表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/database-representation-tabular.md)有关如何创建和操作数据库表示形式的详细说明。  
  
## <a name="connection-representation"></a>连接表示形式  
 连接是指在要包含在表格模型解决方案中的数据与模型之间建立关系。 就 AMO 对象而言，连接与 `xref:Microsoft.AnalysisServices.DataSource` 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据源对象中的所有包含对象可在建模时使用。  
  
 请参阅[连接表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/connection-representation-tabular.md)有关如何创建和操作数据源表示形式的详细说明。  
  
## <a name="table-representation"></a>表的表示形式  
 表是包含数据库中的数据的数据库对象。 就 AMO 对象而言，表具有一对多映射关系。 表表示由以下 AMO 对象的使用情况： `xref:Microsoft.AnalysisServices.DataSourceView`， `xref:Microsoft.AnalysisServices.Dimension`， `xref:Microsoft.AnalysisServices.Cube`， `xref:Microsoft.AnalysisServices.CubeDimension`，`xref:Microsoft.AnalysisServices.MeasureGroup`和`xref:Microsoft.AnalysisServices.Partition`是所需的主要对象。 但是，务必请注意，这并不意味着在建模时，可以使用前面所述的 AMO 对象中包含的所有对象。  
  
 请参阅[表表示&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-representation-tabular.md)有关如何创建和操作的表表示的详细说明。  
  
### <a name="calculated-column-representation"></a>计算列表示形式  
 计算列是用于在表中生成列的计算表达式，其中，将为表中的每个行计算并存储一个新值。 在 AMO 对象方面计算的列具有一个对多映射关系。 通过使用以下 AMO 对象来表示计算列：`xref:Microsoft.AnalysisServices.Dimension` 和 `xref:Microsoft.AnalysisServices.MeasureGroup` 是主要的必需对象。 请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
 请参阅[计算列表示&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-column-representation.md)有关如何创建和操作的计算的列表示的详细说明。  
  
### <a name="calculated-measure-representation"></a>计算度量值表示形式  
 计算度量值是在部署模型后根据请求计算的存储表达式。 就 AMO 对象而言，计算度量值具有一对多映射关系。 通过使用以下 AMO 对象来表示计算列：`xref:Microsoft.AnalysisServices.MdxScript.Commands%2A` 和 `xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A` 是主要的必需对象。 请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
> [!NOTE]  
>  `xref:Microsoft.AnalysisServices.Measure` 对象与表格模型中的计算度量值无关，在表格模型中不支持这些对象。  
  
 请参阅[计算度量值表示&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-measure-representation.md)有关如何创建和操作的计算度量值表示的详细说明。  
  
### <a name="hierarchy-representation"></a>层次结构表示形式  
 层次结构是一种机制，它为最终用户提供了更丰富的浅化和深化体验。 就 AMO 对象而言，层次结构表示形式与 `xref:Microsoft.AnalysisServices.Hierarchy` 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在执行表格建模时使用。  
  
 请参阅[层次结构表示&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-hierarchy-representation.md)有关如何创建和操作的层次结构表示的详细说明。  
  
### <a name="key-performance-indicator-kpi--representation"></a>关键绩效指标 (KPI) 表示形式  
 KPI 用于根据目标值度量基础度量值定义的值的性能。 就 AMO 对象而言，KPI 表示形式具有一对多映射关系。 由以下 AMO 对象的使用情况表示 KPI:`xref:Microsoft.AnalysisServices.MdxScript.Commands%2A`和`xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A`是所需的主要对象。  请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
> [!NOTE]  
>  此外，很重要的一点区别是：`xref:Microsoft.AnalysisServices.Kpi` 对象与表格模型中的 KPI 无关。 而且，在表格模型中也不支持这些对象。  
  
 请参阅[关键绩效指标表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-key-performance-indicator-representation.md)有关如何创建和操作的 KPI 表示的详细说明。  
  
### <a name="partition-representation"></a>分区表示形式  
 用于操作的目的，可以在不同的子集划分表行，当组合在一起，构成表。 其中的每个子集都是表的一个分区。 在 AMO 对象方面分区表示形式具有一对一映射关系`xref:Microsoft.AnalysisServices.Partition`并且任何其他主要的 AMO 对象是必需的。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在建模时使用。  
  
 请参阅[分区表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-partition-representation.md)有关如何创建和操作分区表示形式的详细说明。  
  
## <a name="relationship-representation"></a>关系表示形式  
 关系是两个数据表之间的联系。 该关系确立两个表中的数据应该如何相关。  
  
 在表格模型中，两个表之间可以定义多重关系。 定义两个表之间的多个关系时，只有一个关系可被定义为默认活动关系。 所有其他关系处于不活动状态。  
  
 就 AMO 对象而言，所有不活动关系与 `xref:Microsoft.AnalysisServices.Relationship` 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 对于活动关系，存在其他要求，且需要到 `xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension` 的映射。 请注意，这并不意味着 AMO 关系或 referenceMeasureGroupDimension 对象中的所有包含对象可在建模时使用。  
  
 请参阅[关系表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md)有关如何创建和操作关系表示形式的详细说明。  
  
## <a name="perspective-representation"></a>透视表示形式  
 透视是用于简化或聚焦模式的机制。 就 AMO 对象而言，关系表示形式与 `xref:Microsoft.AnalysisServices.Perspective` 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请务必注意，这并不意味着执行表格建模时，可以使用 AMO 透视对象中包含的所有对象。  
  
 请参阅[透视表示形式&#40;表格&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/perspective-representation-tabular.md)有关如何创建和操作透视表示形式的详细说明。  
  
> [!WARNING]  
>  透视并不是一种安全机制；用户仍可通过其他接口访问透视外部的对象。  
  
  
