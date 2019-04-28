---
title: 挖掘模型 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services]
- logical architecture [Analysis Services Multidimensional Data]
- properties [Analysis Services]
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: cd4df273-0c6a-4b3e-9572-8a7e313111e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bf91af4556694ea032dccd8d502e4480fc4c750
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733767"
---
# <a name="mining-models-analysis-services---data-mining"></a>挖掘模型（Analysis Services - 数据挖掘）
  “挖掘模型”是通过将算法应用于数据创建的  ，但挖掘模型并不仅仅是算法或元数据容器：它是可应用于新数据以便生成预测和对关系进行推断的数据、统计信息和模式的集合。  
  
 本节解释什么是数据挖掘模型以及它可用于的对象：模型和结构的基本体系结构、挖掘模型的属性以及创建和使用挖掘模型的方式。  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
 [定义数据挖掘模型](#bkmk_mdlDefine)  
  
 [挖掘模型属性](#bkmk_mdlProps)  
  
 [挖掘模型列](#bkmk_mdlCols)  
  
 [处理挖掘模型](#bkmk_mdlProcess)  
  
 [查看和查询挖掘模型](#bkmk_mdlView)  
  
##  <a name="bkmk_mdlArch"></a> 挖掘模型体系结构  
 数据挖掘模型从挖掘结构中获取数据，然后使用数据挖掘算法分析这些数据。 挖掘结构和挖掘模型是单独的对象。 挖掘结构存储定义数据源的信息。 挖掘模型存储通过数据的统计处理而得到的信息，例如发现的模式，即分析结果。  
  
 在处理并分析挖掘结构所提供的数据之前，挖掘模型一直为空。 在处理挖掘模型之后，该模型将包含元数据、结果和指回到挖掘结构的绑定。  
  
 ![模型包含元数据、 模式和绑定](../media/dmcon-modelarch2.gif "模型包含元数据、 模式和绑定")  
  
 元数据指定模型的名称和存储模型的服务器以及模型的定义，包括生成模型时所使用的挖掘结构中的列、处理模型时应用的任何筛选器的定义以及用于分析数据的算法。 所有这些选择的数据列并且其数据类型、 筛选器和算法具有极大地影响分析结果。  
  
 例如，您可以使用相同的数据来创建多个模型，并且可以使用聚类分析算法、决策树算法和 Naïve Bayes 算法。 每种模型类型都可以创建可用于进行预测的模式、项集、规则或公式的不同集合。 通常，每个算法都以不同方式对数据进行分析，因此，生成的模型的“内容”  也按不同的结构进行组织。 在一种模型中，数据和模式可以按“分类” 进行分组；在另一种模型中，数据可以组织为对其进行划分和定义的树、分支和规则。  
  
 该模型还受到您对其进行定型的数据的影响：如果您以不同方式筛选数据或者在分析过程中使用不同的种子，则甚至是对相同挖掘结构进行定型的模型也会生成不同结果。 但是，实际数据不存储在仅限模型的摘要统计信息存储，而实际数据驻留在挖掘结构中。 如果您已在定型时对数据创建了筛选器，则筛选器定义也与模型对象一起保存。  
  
 该模型将包含一组绑定，这些绑定将指回到挖掘结构中缓存的数据。 如果已在结构中缓存数据，但在处理后未清除这些数据，则使用这些绑定可以从结果钻取到支持这些结果的事例。 但是，实际数据存储在结构缓存中，而不是模型中。  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlDefine"></a> 定义数据挖掘模型  
 您可以通过执行下面的一般步骤来创建数据挖掘模型：  
  
-   创建基础挖掘结构，包括可能需要的数据列。  
  
-   选择最适合于分析任务的算法。  
  
-   选择结构，使用在模型中，并指定要如何在使用此列中的列包含你想要预测的结果哪些列仅用于输入，依此类推。  
  
-   （可选）设置参数以微调算法所执行的处理。  
  
-   通过处理  结构和模型，使用数据填充模型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供下列可帮助您管理挖掘模型的工具：  
  
-   数据挖掘向导可帮助您创建结构和相关挖掘模型。 这是最简单的使用方法。 该向导自动创建所需的挖掘结构，并帮助您配置重要设置。  
  
-   DMX CREATE MODEL 语句可用于定义模型。 所需结构将作为过程的一部分自动创建；因此，不能利用该方法重用现有结构。 如果您已确切知道要创建哪种模型，或者您想要编写模型脚本，请使用此方法。  
  
-   DMX ALTER STRUCTURE ADD MODEL 语句可用于向现有结构中添加新的挖掘模型 如果要基于相同数据集试验不同模型，请使用此方法。  
  
 还可以通过编程方式、使用 AMO 或 XML/A 或者使用 Excel 数据挖掘客户端等其他客户端创建挖掘模型。 有关详细信息，请参阅下列主题：  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProps"></a> 挖掘模型属性  
 每个挖掘模型都具有用于定义该模型及其元数据的属性。 这些属性包括名称、说明、上次处理模型的日期、对模型的权限以及针对用于定型的数据的任何筛选器。  
  
 每个挖掘模型还具有派生自挖掘结构且说明该模型使用的数据列的属性。 如果模型使用的任何列为嵌套表，则该列还可以应用单独的筛选器。  
  
 此外，每个挖掘模型还包含两个特殊属性： <xref:Microsoft.AnalysisServices.MiningModel.Algorithm%2A> 和 <xref:Microsoft.AnalysisServices.MiningModelColumn.Usage%2A>。  
  
-   **Algorithm 属性** 指定创建模型所使用的算法。 可用的算法取决于您所使用的访问接口。 有关所含的算法的列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请参阅[Data Mining Algorithms &#40;Analysis Services-数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)。 `Algorithm` 属性应用于挖掘模型，并且对于每个模型，只能设置该属性一次。 以后您可以更改算法，但如果挖掘模型中的某些列不受您所选算法的支持，则这些列可能会无效。 在对此属性进行更改后，您必须始终重新处理该模型。  
  
-   **Usage 属性** 定义模型使用每个列的方式。 您可以将列用法定义为 `Input`、`Predict`、`Predict Only` 或 `Key`。 `Usage` 属性应用于挖掘模型的各个列，且必须为模型中包含的每个列分别设置此属性。 如果结构包含在模型中不使用的列，则用法设置为 `Ignore`。 您可以在挖掘结构中包括、但不在分析中使用的数据示例可以是客户名称或电子邮件地址。 这样，您可以在以后查询它们，而不必在分析阶段包括它们。  
  
 创建挖掘模型后，您可以更改挖掘模型属性的值。 但是，只要进行了更改（甚至包括对挖掘模型名称的更改），就需要重新处理模型。 在重新处理模型后，可能会显示不同的结果。  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlCols"></a> 挖掘模型列  
 挖掘模型包含从挖掘结构中定义的列获取的数据列。 您可以选择要在模型中使用的挖掘结构中的列，并且可以创建挖掘结构列的副本，然后对其进行重命名或更改其用法。 作为模型生成过程的一部分，您还必须定义模型对列的用法。 这包含如下信息：列是否为键、列是否用于预测或算法是否可忽略列。  
  
 在您生成模型时，而非自动添加每个可用数据列时，建议您仔细查看结构中的数据，并且在模型中仅包含对分析有意义的那些列。 例如，您应该避免包含重复相同数据的多列，并且应该避免使用具有最多唯一值的列。 如果您认为不应当使用某个列，不需要从挖掘结构或挖掘模型中删除该列；您只需对该列设置一个标志，指定在生成模型时应忽略该列。 这意味着该列将保留在挖掘结构中，但将不会用在挖掘模型中。 如果您已启用了从模型到挖掘结构的钻取，则可以在以后从该列检索信息。  
  
 根据选择的算法，挖掘结构中的某些列可能与某些模型类型不兼容，或者可能向您提供不良结果。 例如，如果数据包含连续数值数据（例如收入列），并且您的模型要求离散值，则可能需要将数据转换为离散范围或从模型中删除数据。 在某些情况下，该算法将自动为您转换数据数据，但结果不见得始终是您想要的结果或预期的结果。 考虑创建列的附加副本，并尝试不同的模型。 您还可以对单独的列设置标志，以便指示需要特殊处理的地方。 例如，如果您的数据包含 Null 值，则可以使用建模标志来控制处理。 如果您想要将特定列视作模型中的回归量，则可以使用建模标志来这样做。  
  
 在创建模型之后，可以进行添加或删除列等更改，或者更改模型的名称。 但是，任何更改（甚至包括仅模型元数据的更改）都需要重新处理模型。  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProcess"></a> 处理挖掘模型  
 在处理之前，数据挖掘模型是一个空对象。 处理模型时，结构缓存的数据将通过筛选器进行传递（如果已在模型中定义了筛选器），并通过算法进行分析。 算法将计算描述数据的一组汇总统计信息，确定数据中的规则和模式，然后使用这些规则和模式填充模型。  
  
 在处理后，挖掘模型将包含与通过分析发现的数据和模式有关的大量信息，包括统计信息、规则和递归公式。 您可以使用自定义查看器来浏览此信息，或者可以创建数据挖掘查询以便检索此信息并将其用于分析和展示。  
  
 [挖掘模型体系结构](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlView"></a> 查看和查询挖掘模型  
 在处理模型后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的自定义查看器来浏览此模型。 For  
  
 还可以针对挖掘模型创建查询以进行预测或检索由模型创建的模型元数据或模式。 使用数据挖掘扩展插件 (DMX) 创建查询。  
  
## <a name="related-content"></a>相关内容  
  
|主题|链接|  
|------------|-----------|  
|了解如何构建可以支持多个挖掘模型的挖掘结构。 了解模型中的列用法。|[挖掘结构列](mining-structure-columns.md)<br /><br /> [挖掘模型列](mining-model-columns.md)<br /><br /> [内容类型（数据挖掘）](content-types-data-mining.md)|  
|了解不同的算法，以及所选算法是如何影响模型内容的。|[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)<br /><br /> [数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)|  
|了解如何设置将影响其组成和行为的模型的属性。|[挖掘模型属性](mining-model-properties.md)<br /><br /> [建模标志（数据挖掘）](modeling-flags-data-mining.md)|  
|了解用于数据挖掘的可编程接口。|[使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)<br /><br /> [数据挖掘扩展插件 (DMX) 参考](/sql/dmx/data-mining-extensions-dmx-reference)|  
|了解如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的自定义数据挖掘查看器。|[数据挖掘模型查看器](data-mining-model-viewers.md)|  
|查看可针对数据挖掘模型使用的不同查询类型的示例。|[数据挖掘查询](data-mining-queries.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
 使用下面的链接可以获取有关使用数据挖掘模型的更具体信息  
  
|任务|链接|  
|----------|----------|  
|添加和删除挖掘模型|[在现有挖掘结构中添加挖掘模型](add-a-mining-model-to-an-existing-mining-structure.md)<br /><br /> [从挖掘结构中删除挖掘模型](delete-a-mining-model-from-a-mining-structure.md)|  
|使用挖掘模型列|[从挖掘模型中排除列](exclude-a-column-from-a-mining-model.md)<br /><br /> [为模型列创建别名](create-an-alias-for-a-model-column.md)<br /><br /> [更改挖掘模型中列的离散化](change-the-discretization-of-a-column-in-a-mining-model.md)<br /><br /> [在模型中指定用作回归量的列](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|更改模型属性|[更改挖掘模型的属性](change-the-properties-of-a-mining-model.md)<br /><br /> [对挖掘模型应用筛选器](apply-a-filter-to-a-mining-model.md)<br /><br /> [从挖掘模型中删除筛选器](delete-a-filter-from-a-mining-model.md)<br /><br /> [对挖掘模型启用钻取](enable-drillthrough-for-a-mining-model.md)<br /><br /> [查看或更改算法参数](view-or-change-algorithm-parameters.md)|  
|复制、 移动或管理模型|[生成挖掘模型的副本](make-a-copy-of-a-mining-model.md)<br /><br /> [复制挖掘模型的视图](copy-a-view-of-a-mining-model.md)<br /><br /> [EXPORT (DMX)](/sql/dmx/export-dmx)<br /><br /> [IMPORT (DMX)](/sql/dmx/import-dmx)|  
|使用数据填充模型，或更新模型中的数据|[处理挖掘模型](process-a-mining-model.md)|  
|使用 OLAP 模型|[创建数据挖掘维度](create-a-data-mining-dimension.md)|  
  
## <a name="see-also"></a>请参阅  
 [数据库对象（Analysis Services - 多维数据）](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
