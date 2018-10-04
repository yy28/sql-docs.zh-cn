---
title: 在多维模型中创建度量值和度量值组 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- measure groups [Analysis Services], defining
ms.assetid: 1018bb2e-b89b-489e-aead-450dec5dca3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8f7e9df6417334b814e71664b2a164dd76a9642
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060359"
---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>在多维模型中创建度量值和度量值组
  *度量值* 是数字数据值的聚合，如求和、计数、最小值、最大值、平均值或你创建的自定义 MDX 表达式。 *度量值组* 是一个或多个度量值的容器。 所有度量值存在于一个度量值组中，即使只有一个度量值。 一个多维数据集必须至少有一个度量值和度量值组。  
  
 本主题包含以下各节：  
  
-   [创建度量值的方法](#bkmk_create)  
  
-   [度量值的组件](#bkmk_comps)  
  
-   [为事实和事实数据表上的度量值和度量值组建模](#bkmk_modeling)  
  
-   [度量值组的粒度](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> 创建度量值的方法  
 度量值可以是数据集中的静态元素，在设计时创建，当数据集被访问时始终存在。 还可以使用 MDX 将度量值定义为 *“计算成员”* ，从而为基于多维数据集中其他度量值的度量值提供计算值。 计算成员的范围可以为会话或用户。  
  
 若要创建一个度量值或度量值组，请使用以下方法之一：  
  
|||  
|-|-|  
|多维数据集向导|在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中运行多维数据集向导以创建多维数据集。<br /><br /> 在“解决方案资源管理器”中，右键单击“多维数据集”，然后选择“新建多维数据集”。 如果在执行这些步骤中需要帮助，请参阅[多维建模（Adventure Works 教程）](../multidimensional-modeling-adventure-works-tutorial.md)。<br /><br /> 创建基于来自现有数据仓库的表的多维数据集时，度量值和度量值组的定义具体化为多维数据集创建过程的一部分。 在向导中，你将选择要用作多维数据集中度量值和度量值组对象的基础的事实和事实数据表。|  
|新建度量值对话|假定 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中已存在该多维数据集，则双击“解决方案资源管理器”中的多维数据集名称，在“多维数据集设计器”中打开该多维数据集。 在“度量值”窗格中，通过指定源表、列和聚合类型，右键单击顶端节点以创建新度量值组或新度量值。 使用此方法需从预构建函数固定列表中选择聚合方法。 有关更常用的聚合的讨论，请参阅 [Use Aggregate Functions](use-aggregate-functions.md) 。|  
|“计算成员”|计算成员会增加 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中多维数据集的灵活性，并提高其分析能力，因为你可以控制创建它们的时间和方式。 有时你只是临时需要一个度量值，需要度量值的时间仅为用户会话持续时间，或需要位于 Management Studio 中作为调查的一部分的度量值。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开“计算”选项卡创建新计算成员。<br /><br /> 度量值基于 MDX 表达式时，请选择这种方法。 有关详细信息，请参阅这些主题：[在 MDX 中生成度量值](mdx/mdx-building-measures.md)、[计算](../multidimensional-models-olap-logical-cube-objects/calculations.md)、[多维模型中的计算](calculations-in-multidimensional-models.md)和 [MDX 脚本编写基础知识 (Analysis Services)](mdx/mdx-scripting-fundamentals-analysis-services.md)。|  
|MDX 或 XMLA|在 SQL Server Management Studio 中，你可以执行 MDX 或 XMLA 以更改数据库，从而以包含新的计算度量值。 在该解决方案已部署到服务器之后，这种方法对数据的临时测试有用。 请参阅 [Document and Script an Analysis Services Database](document-and-script-an-analysis-services-database.md)。|  
  
##  <a name="bkmk_comps"></a> 度量值的组件  
 度量值是具有属性的对象。 除了其名称外，度量值必须具有聚合类型和源列，或具有用于加载具有数据的度量值的表达式。 你可以通过设置度量值属性来修改度量值定义。  
  
|||  
|-|-|  
|**源 (source)**|大多数度量值都来自外部数据仓库的事实数据表中的数值列（比如 AdventureWorks 数据仓库中“Internet 销售”和“分销商销售”表中的“销售额”列），但是你也可以完全根据你定义的计算来创建新度量值。<br /><br /> 维度表中的属性列可以用于定义度量值，但是这些度量值通常在聚合行为方面具有半累加性或非累加性。 有关半累加性行为的详细信息，请参阅 [定义半累加性行为](define-semiadditive-behavior.md)。|  
|**聚合**|默认情况下，度量值按每个维度进行求和。 但是，通过 `AggregateFunction` 属性，您可以修改此行为。 有关列表，请参阅 [Use Aggregate Functions](use-aggregate-functions.md) 。|  
|**属性**|有关附加属性说明，请参阅 [Configure Measure Properties](configure-measure-properties.md) 。|  
  
##  <a name="bkmk_modeling"></a> 为事实和事实数据表上的度量值和度量值组建模  
 在运行向导前，它有助于理解度量值定义的建模原则。  
  
 度量值和度量值组是表示外部数据仓库中的事实和事实数据表的多维对象。 在大多数情况下，度量值和度量值组都将基于数据源视图中的对象，而这些对象是从基础数据仓库创建的。  
  
 下面的关系图表示 **FactSalesQuota** 事实数据表和两个与其关联的维度表： **DimTime** 和 **DimEmployee**。 在 Adventure Works 示例多维数据集中，这些表用作 Sales Quotas 量值组以及 Time 和 Employee 维度的基础。  
  
 ![具有两个维度表的 FactSalesQuota 表](../media/factsalesquota.gif "具有两个维度表的 FactSalesQuota 表")  
  
 事实数据表包含两种基本类型的列：属性列和度量值列。  
  
-   属性列用于创建维度表的外键关系，因此度量值列中的可计量数据可以按照维度表中包含的数据进行组织。 属性列还用于定义事实数据表的粒度及其度量值组。  
  
-   度量值列定义度量值组包含的度量值。  
  
 运行“多维数据集向导”时，会筛选掉外键。在可供选择的剩余列的列表中，你将看到度量值列和未被标识为外键的属性列。 在 **FactSalesQuote** 示例中，除 **SalesAmountQuota** 外，该向导还将提供 **CalendarYear** 和 **CalendarQuarter**。 只有 **SalesAmountQuota** 度量值列将得出多维模型的可操作度量值。 其他基于日期的列用于限定每个配额数量。 你应从“多维数据集向导”中的度量值列表中排除其他列（ **CalendarYear** 和 **CalendarQuarter**），或稍后从“设计器”的度量值组中删除它们。  
  
 本讨论的重点是，并非所有由该向导提供的列都可用作度量值。 决定要将哪些列用作度量值，主要取决于你对数据的理解以及使用数据的方式。 请记住，可以右键单击数据源视图中的表以浏览数据，这可帮助你识别用作度量值的列。 有关详细信息，请参阅[在数据源视图中浏览数据 (Analysis Services)](explore-data-in-a-data-source-view-analysis-services.md)。  
  
> [!NOTE]  
>  不是所有的度量值都是直接从存储在事实数据表列中的值派生而来的。 例如，Adventure Works 示例多维数据集的 **“销售配额”** 度量值组中定义的 **“销售人员计数”** 度量值实际基于 **FactSalesQuota** 事实数据表的 **EmployeeKey** 列中的唯一值计数（或非重复计数）。  
  
##  <a name="bkmk_grain"></a> 度量值组的粒度  
 度量值组具有引用事实数据表支持的详细级别的关联粒度。 通过对维度的外键关系设置粒度。  
  
 例如， **FactSalesQuota** 事实数据表与 **DimEmployee** 表具有外键关系， **FactSalesQuota** 表中的每项记录都与单个雇员相关；因此，从“雇员”维度来查看，该度量值组的粒度处于单个雇员级别。  
  
 度量值组的粒度绝对不能设置为比从中查看该度量值组的维度的最低级别还细，但可以使用其他属性将该粒度设置为更粗。 例如， **FactSalesQuota** 事实数据表使用三列（ **TimeKey**、 **CalendarYear**和 **CalendarQuarter**）来建立与 **DimTime** 表的关系的粒度。 因此，从“时间”维度来查看，度量值组的粒度是按日历季度（而不是按“时间”维度的最低级别，即“天”）来确定的。  
  
 您可以通过使用多维数据集设计器的 **“维度用法”** 选项卡来指定与特定维度相关的度量值组的粒度。 有关维度关系的详细信息，请参阅 [Dimension Relationships](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的多维数据集](cubes-in-multidimensional-models.md)   
 [度量值和度量值组](measures-and-measure-groups.md)  
  
  
