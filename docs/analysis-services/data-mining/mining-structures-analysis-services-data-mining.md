---
title: "挖掘结构 (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- mining structures [Analysis Services], about mining structures
- mining structures [Analysis Services]
- data mining [Analysis Services], structure
- Analysis Services objects, data mining objects
- data mining [Analysis Services], models
- algorithms [data mining]
- data mining [Analysis Services], objects
- mining models [Analysis Services]
- mining models [Analysis Services], about data mining models
ms.assetid: 39748290-c32a-48e6-92a6-0c3a9223773a
caps.latest.revision: "77"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9d796c274172d6fdc8402c5965b6d281cc8c4e89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mining-structures-analysis-services---data-mining"></a>挖掘结构（Analysis Services – 数据挖掘）
  挖掘结构定义生成挖掘模型时依据的数据：它指定源数据视图、列数量和类型以及分为定型集和测试集的可选分区。 单个挖掘结构可以支持多个共享同一个域的挖掘模型。 下图说明了数据挖掘结构与数据源以及构成数据挖掘模型之间的关系。  
  
 ![处理的数据： 源模型的结构到](../../analysis-services/data-mining/media/dmcon-modelarch.gif "处理的数据： 源到模型的结构")  
  
 关系图中的挖掘结构基于包含多个表或视图的数据源，它们按 CustomerID 字段进行联接。 一个表包含有关客户的信息，例如地理区域、年龄、收入和性别，而相关嵌套表包含每个客户的多行其他相关信息，例如客户已购买的产品。 此关系图显示根据一个挖掘结构可以生成多个模型，并且这些模型可以使用该结构中的不同列。  
  
 **模型 1** 使用 CustomerID、收入、年龄和区域，并根据区域筛选数据。  
  
 **模型 2** 使用 CustomerID、收入、年龄和区域，并根据年龄筛选数据。  
  
 **模型 3** 使用 CustomerID、年龄、性别和嵌套表，不使用筛选器。  
  
 由于以上模型使用不同的输入列，并且其中两个模型还通过应用筛选器来限制在模型中使用的数据，因此即使这些模型基于相同数据，其结果也将大不相同。 请注意，CustomerID 列在所有模型中都是必需的，因为它是可作为事例键使用的唯一可用列。  
  
 本节说明数据挖掘结构的基本体系结构：如何定义挖掘结构、如何用数据填充它以及如何使用它创建模型。 有关如何管理或导出现有数据挖掘结构的详细信息，请参阅 [管理数据挖掘解决方案和对象](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)。  
  
## <a name="defining-a-mining-structure"></a>定义挖掘结构  
 建立数据挖掘结构涉及到下列步骤：  
  
-   定义数据源。  
  
-   选择要包含在结构中的数据列（只需要将一部分列添加到模型），然后定义键。  
  
-   定义结构的键，包括嵌入表的键（如果适用）。  
  
-   指定是否应将源数据分为定型集和测试集。 此步骤为可选步骤。  
  
-   处理结构。  
  
 这些步骤将在以下各节中进行详细说明。  
  
### <a name="data-sources-for-mining-structures"></a>挖掘结构的数据源  
 在定义挖掘结构时，可以使用现有数据源视图中的列。 数据源视图是一个共享对象，允许您合并多个数据源并将它们作为单个源使用。 原始数据源对客户端应用程序不可见，您可以使用数据源视图的属性修改数据类型、创建聚合或别名列。  
  
 如果您按照同一个挖掘结构生成多个挖掘模型，则这些模型可以使用该结构中的不同列。 例如，可以创建单个结构，然后基于该结构生成单独的决策树和聚类分析模型，每个模型都使用不同的列并预测不同的属性。  
  
 此外，每个模型可以以不同的方式使用结构中的列。 例如，您的数据源视图可能包含“收入”列，您可以以不同方式在不同的模型中使用它。  
  
 数据挖掘结构采用源数据的“绑定”  形式存储数据源的定义和其中的列。 有关数据源绑定的详细信息，请参阅[数据源和绑定（SSAS 多维）](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。 不过，请注意，你还可以使用 DMX [CREATE MINING STRUCTURE (DMX)](../../dmx/create-mining-structure-dmx.md) 语句创建数据挖掘结构，而不需要将该结构绑定到特定数据源。  
  
### <a name="mining-structure-columns"></a>挖掘结构列  
 挖掘结构的构造块是挖掘结构列，这些列对数据源所包含的数据进行说明。 这些列包含诸如数据类型、内容类型以及数据分发方式等信息。 挖掘结构不包含有关如何在特定挖掘模型中使用列的信息，也不包含有关用于生成模型的算法类型的信息；这些信息在挖掘模型本身中进行定义。  
  
 挖掘结构也可包含嵌套表。 嵌套表表示事例实体与其相关属性之间的一对多关系。 例如，如果客户说明信息位于一个表中，而客户采购信息位于另一个表中，则可使用嵌套表将这些信息组合到一个事例中。 客户标识符是实体，采购信息是相关属性。 有关何时使用嵌套表的详细信息，请参阅[嵌套表（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
 要在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建数据挖掘模型，必须首先创建一个数据挖掘结构。 数据挖掘向导可引导您完成创建挖掘结构、选择数据和添加挖掘模型的整个过程。  
  
 如果使用数据挖掘扩展插件 (DMX) 创建挖掘模型，您可以指定该模型及其包含的列，然后 DMX 将自动创建所需挖掘结构。 有关详细信息，请参阅 [CREATE MINING MODEL (DMX)](../../dmx/create-mining-model-dmx.md)。  
  
 有关详细信息，请参阅 [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md)。  
  
### <a name="dividing-the-data-into-training-and-testing-sets"></a>将数据分为定型集和测试集  
 在为挖掘结构定义数据时，还可以指定将一些数据用于定型并将另一些数据用于测试。 因此，在创建数据挖掘结构之前，无须再对数据进行拆分。 在创建模型时，您可以指定将一定百分比的数据用于测试并将其余数据用于定型，也可以指定将一定数量的事例用作测试数据集。 有关定型数据集和测试数据集的信息随挖掘结构一起存储，因此，同一测试集可以与基于该结构的所有模型一起使用。  
  
 有关详细信息，请参阅 [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
### <a name="enabling-drillthrough"></a>启用钻取  
 即使您不打算在特定的挖掘模型中使用某列，也可以将该列添加到挖掘结构中。 例如，如果您要在聚类分析模型中检索客户的电子邮件地址而在分析过程中不使用电子邮件地址，这很有用。 为了在分析和预测阶段忽略某列，您将该列添加到结构但是不指定它的用途，或将使用标志设置为“忽略”。 如果对挖掘模型启用了钻取功能并且您具有相应的权限，则以这种方式标记的数据仍可以在查询中使用。 例如，您可以查看分析所有客户后的分类结果，然后使用钻取查询获取特定分类中客户的姓名和电子邮件地址，即使这些数据列不用于生成模型。  
  
 有关详细信息，请参阅[钻取查询（数据挖掘）](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
### <a name="processing-mining-structures"></a>处理挖掘结构  
 挖掘结构在处理之前只是一个元数据容器。 当您处理挖掘结构时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会创建一个缓存，用于存储有关数据的统计信息、如何离散化任何连续属性的信息以及挖掘模型以后要使用的其他信息。 挖掘模型本身不存储此摘要信息，而是在处理挖掘结构时引用缓存的信息。 因此，您不必在每次向现有结构中添加新模型时重新处理结构；可以只处理模型。  
  
 如果缓存很大或您要删除详细数据，可以选择在处理后丢弃此缓存。 如果您不希望缓存数据，则可以将挖掘结构的 **CacheMode** 属性更改为 **ClearAfterProcessing**。 这将导致在处理所有模型之后销毁缓存。 将 **CacheMode** 属性设置为 **ClearAfterProcessing** 将禁止从挖掘模型钻取。  
  
 但是，在破坏缓存后，将无法向挖掘结构添加新模型。 如果向该结构中添加新的挖掘模型或更改现有模型的属性，将需要首先重新处理挖掘结构。 有关详细信息，请参阅[处理要求和注意事项（数据挖掘）](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
### <a name="viewing-mining-structures"></a>查看挖掘结构  
 不能使用查看器来浏览挖掘结构中的数据。 但是，在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，可以使用数据挖掘设计器的 **“挖掘结构”** 选项卡来查看结构列及其定义。 有关详细信息，请参阅 [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md)。  
  
 如果您希望查看挖掘结构中的数据，则可以使用数据挖掘扩展插件 (DMX) 来创建查询。 例如， `SELECT * FROM <structure>.CASES` 语句返回挖掘结构中的所有数据。 若要检索此信息，必须处理挖掘结构，并且必须缓存处理结果。  
  
 `SELECT * FROM <model>.CASES` 语句返回相同的列，但是仅针对该特定模型中的事例返回。 有关详细信息，请参阅 [SELECT FROM <结构>.CASES](../../dmx/select-from-structure-cases.md) 和 [SELECT FROM <模型>.CASES (DMX)](../../dmx/select-from-model-cases-dmx.md)。  
  
## <a name="using-data-mining-models-with-mining-structures"></a>在挖掘结构中使用数据挖掘模型  
 数据挖掘模型为挖掘结构表示的数据应用挖掘模型算法。 挖掘模型是属于特定挖掘结构的对象，并且模型继承由挖掘结构定义的所有属性值。 该模型可以使用挖掘结构包含的所有列，或使用其中一部分列。 可以向挖掘结构中添加某个结构列的多个副本。 还可以向挖掘模型中添加某个结构列的多个副本，然后向该模型中的每个结构列赋予不同的名称或别名 。 有关为结构列创建别名的详细信息，请参阅[为模型列创建别名](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)和[挖掘模型属性](../../analysis-services/data-mining/mining-model-properties.md)。  
  
 有关数据挖掘模型的体系结构的详细信息，请参阅 [挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)。  
  
## <a name="related-tasks"></a>相关任务  
 使用提供的链接了解有关如何定义、管理和使用挖掘结构的详细信息。  
  
|“任务”|链接|  
|-----------|-----------|  
|使用关系挖掘结构|[创建新的关系挖掘结构](../../analysis-services/data-mining/create-a-new-relational-mining-structure.md)<br /><br /> [向挖掘结构中添加嵌套表](../../analysis-services/data-mining/add-a-nested-table-to-a-mining-structure.md)|  
|使用基于 OLAP 多维数据集的挖掘结构|[创建新的 OLAP 挖掘结构](../../analysis-services/data-mining/create-a-new-olap-mining-structure.md)|  
|使用挖掘结构中的列|[向挖掘结构中添加列](../../analysis-services/data-mining/add-columns-to-a-mining-structure.md)<br /><br /> [从挖掘结构中删除列](../../analysis-services/data-mining/remove-columns-from-a-mining-structure.md)|  
|更改或查询挖掘结构属性和数据|[更改挖掘结构的属性](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
|使用基础数据源和更新源数据|[编辑用于挖掘结构的数据源视图](../../analysis-services/data-mining/edit-the-data-source-view-used-for-a-mining-structure.md)<br /><br /> [处理挖掘结构](../../analysis-services/data-mining/process-a-mining-structure.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据库对象（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
