---
title: 了解表格对象模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 574614976a9d24f6c9cedbfede2fd5a150211416
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52525787"
---
# <a name="understanding-the-tabular-object-model"></a>了解表格对象模型
  表格模型是表、关系、层次结构、透视、度量值和关键绩效的逻辑表示形式。 本节介绍使用 AMO 的内部实现。 请参阅[使用分析管理对象开发&#40;AMO&#41; ](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)如果你未使用过 AMO 之前。  
  
 此处的方法是自上而下的，表格模型中的所有相关对象逻辑上映射到 AMO 对象，并说明所需的交互或工作流。 可从 Codeplex 获取使用 AMO 创建表格模型的源代码示例“AMO 到表格”。 请注意，示例中的代码仅作为对此处所述逻辑概念的支持提供，不应用于生产环境中。 不提供对示例的支持或保修。  
  
## <a name="database-representation"></a>数据库表示形式  
 数据库为表格模型提供容器对象。 表格模型中的所有对象包含在数据库中。 就 AMO 对象而言，数据库表示形式与 <xref:Microsoft.AnalysisServices.Database> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在建模时使用。  
  
 请参阅[数据库表示形式&#40;表格&#41;](database-representation-tabular.md)有关的详细说明如何创建和操作数据库表示形式。  
  
## <a name="connection-representation"></a>连接表示形式  
 连接是指在要包含在表格模型解决方案中的数据与模型之间建立关系。 就 AMO 对象而言，连接与 <xref:Microsoft.AnalysisServices.DataSource> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据源对象中的所有包含对象可在建模时使用。  
  
 请参阅[连接表示形式&#40;表格&#41;](connection-representation-tabular.md)有关的详细说明如何创建和操作数据源表示形式。  
  
## <a name="table-representation"></a>表的表示形式  
 表是包含数据库中的数据的数据库对象。 就 AMO 对象而言，表具有一对多映射关系。 通过使用以下 AMO 对象来表示表：<xref:Microsoft.AnalysisServices.DataSourceView>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.CubeDimension>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition> 是主要的必需对象；但是，请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
 请参阅[表表示形式&#40;表格&#41;](tables-representation-tabular.md)有关的详细说明如何创建和操作表的表示形式。  
  
### <a name="calculated-column-representation"></a>计算列表示形式  
 计算列是用于在表中生成列的计算表达式，其中，将为表中的每个行计算并存储一个新值。 就 AMO 对象而言，计算列具有一对多映射关系。 通过使用以下 AMO 对象来表示计算列：<xref:Microsoft.AnalysisServices.Dimension> 和 <xref:Microsoft.AnalysisServices.MeasureGroup> 是主要的必需对象。 请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
 请参阅[计算列表示形式&#40;表格&#41;](tables-calculated-column-representation.md)有关的详细说明如何创建和操作计算的列表示形式。  
  
### <a name="calculated-measure-representation"></a>计算度量值表示形式  
 计算度量值是在部署模型后根据请求计算的存储表达式。 就 AMO 对象而言，计算度量值具有一对多映射关系。 通过使用以下 AMO 对象来表示计算列：<xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> 和 <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> 是主要的必需对象。 请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.Measure> 对象与表格模型中的计算度量值无关，在表格模型中不支持这些对象。  
  
 请参阅[计算度量值表示形式&#40;表格&#41;](tables-calculated-measure-representation.md)有关的详细说明如何创建和操作计算度量值表示形式。  
  
### <a name="hierarchy-representation"></a>层次结构表示形式  
 层次结构是一种机制，它为最终用户提供了更丰富的浅化和深化体验。 就 AMO 对象而言，层次结构表示形式与 <xref:Microsoft.AnalysisServices.Hierarchy> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在执行表格建模时使用。  
  
 请参阅[层次结构表示形式&#40;表格&#41;](tables-hierarchy-representation.md)有关的详细说明如何创建和操作层次结构表示形式。  
  
### <a name="key-performance-indicator--kpi--representation"></a>关键绩效指标表示形式的 KPI  
 KPI 用于根据目标值度量基础度量值定义的值的性能。 就 AMO 对象而言，KPI 表示形式具有一对多映射关系。 通过使用以下 AMO 对象来表示 KPI：<xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> 和 <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> 是主要的必需对象。  请注意，这并不意味着前面提到的 AMO 对象中的所有包含对象可在建模时使用。  
  
> [!NOTE]  
>  此外，很重要的一点区别是：<xref:Microsoft.AnalysisServices.Kpi> 对象与表格模型中的 KPI 无关。 而且，在表格模型中也不支持这些对象。  
  
 请参阅[关键绩效指标表示形式&#40;表格&#41;](tables-key-performance-indicator-representation.md)有关的详细说明如何创建和操作 KPI 表示形式。  
  
### <a name="partition-representation"></a>分区表示形式  
 为便于操作，可以将一个表划分为不同的行子集，而将这些行子集组合在一起可形成表。 其中的每个子集都是表的一个分区。 就 AMO 对象而言，分区表示形式与 <xref:Microsoft.AnalysisServices.Partition> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 数据库对象中的所有包含对象可在建模时使用。  
  
 请参阅[分区表示形式&#40;表格&#41;](tables-partition-representation.md)有关的详细说明如何创建和操作分区表示形式。  
  
## <a name="relationship-representation"></a>关系表示形式  
 关系是两个数据表之间的联系。 该关系确立两个表中的数据应该如何相关。  
  
 在表格模型中，两个表之间可以定义多重关系。 定义两个表之间的多个关系时，只有一个关系可被定义为默认活动关系。 所有其他关系处于不活动状态。  
  
 就 AMO 对象而言，所有不活动关系与 <xref:Microsoft.AnalysisServices.Relationship> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 对于活动关系，存在其他要求，且需要到 <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> 的映射。 请注意，这并不意味着 AMO 关系或 referenceMeasureGroupDimension 对象中的所有包含对象可在建模时使用。  
  
 请参阅[关系表示形式&#40;表格&#41;](relationship-representation-tabular.md)有关的详细说明如何创建和操作关系表示形式。  
  
## <a name="perspective-representation"></a>透视表示形式  
 透视是用于简化或聚焦模式的机制。 就 AMO 对象而言，关系表示形式与 <xref:Microsoft.AnalysisServices.Perspective> 之间存在一对一映射关系，并且不需要任何其他主要 AMO 对象。 请注意，这并不意味着 AMO 透视对象中的所有包含对象可在执行表格建模时使用。  
  
 请参阅[透视表示形式&#40;表格&#41;](perspective-representation-tabular.md)有关的详细说明如何创建和操作透视表示形式。  
  
> [!WARNING]  
>  透视并不是一种安全机制；用户仍可通过其他接口访问透视外部的对象。  
  
  
