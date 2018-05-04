---
title: 逻辑体系结构 (Analysis Services-数据挖掘) |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2ff8521531c470ed485e20b71d1d0b0dbfbbd9a2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="logical-architecture-analysis-services---data-mining"></a>逻辑体系结构（Analysis Services - 数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  数据挖掘过程涉及多个组件的交互。  
  
-   您可以访问 SQL Server 数据库中的数据源或任何其他数据源，以便用于定型、测试或预测。  
  
-   使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 Visual Studio 可以定义数据挖掘结构和模型。  
  
-   您通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来管理数据挖掘对象，并创建预测和查询。  
  
-   完成解决方案之后，您可以将其部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。  
  
 已在其他地方介绍创建这些解决方案对象的过程。 有关详细信息，请参阅 [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
 以下章节说明数据挖掘解决方案中对象的逻辑体系结构。  
  
 [数据挖掘源数据](#bkmk_SourceData)  
  
 [挖掘结构](#bkmk_Structures)  
  
 [挖掘模型](#bkmk_Models)  
  
 [自定义数据挖掘对象](#bkmk_CustomObjects)  
  
##  <a name="bkmk_SourceData"></a> 数据挖掘源数据  
 在数据挖掘中使用的数据并不会存储在数据挖掘解决方案中，而仅存储绑定。 该数据可能驻留在 SQL Server 早期版本创建的数据库、CRM 系统，或者甚至平面文件中。 通过处理定型结构或模型时，将创建数据的统计汇总并在缓存中存储它，这样可以将其持久化以供以后的操作使用它；或者在处理后删除数据的统计汇总。 有关详细信息，请参阅[挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源视图 (DSV) 对象中组合不同数据，将在你的数据源上提供一个抽象层。 您可以指定表之间的联接，或添加具有多对一关系的表以便创建嵌套表列。 这些对象的定义、数据源和数据源视图存储在解决方案内，文件扩展名为 *.ds 和 \*.dsv。 有关创建和使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源以及数据源视图的详细信息，请参阅[支持的数据源（SSAS - 多维）](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)。  
  
 还可以使用 AMO 或 XMLA 定义和更改数据源以及数据源视图。 有关以编程方式使用这些对象的详细信息，请参阅[逻辑体系结构概述（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)。  
  
  
##  <a name="bkmk_Structures"></a> Mining Structures  
 数据挖掘结构是一种逻辑数据容器，它定义从中生成挖掘模型的数据域。 单个挖掘结构可以支持多个挖掘模型。  
  
 需要使用数据挖掘解决方案中的数据时，Analysis Services 读取源的数据并生成聚合以及其他信息的缓存。 默认情况下，将此缓存持久化以便可以重用定型数据来支持其他模型。 如果您需要删除此缓存，请将挖掘结构对象的 **CacheMode** 属性更改为值 **ClearAfterProcessing**。 有关详细信息，请参阅 [AMO 数据挖掘类](../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)。  
  
 Analysis Services 还提供了将你的数据分开分为定型集和测试数据集，以便你可以测试挖掘模型上一套代表性、 随机选择的数据的能力。 数据实际未单独存储；使用一个属性标记结构缓存中的事例数据，该属性指示特定事例是用于定型还是测试。 如果删除缓存，则无法检索该信息。  
  
 有关详细信息，请参阅[挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 数据挖掘结构可包含嵌套表。 嵌套表提供有关在主要数据表中建模的事例的其他详细信息。 有关详细信息，请参阅[嵌套表（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
##  <a name="bkmk_Models"></a> Mining Models  
 处理前，数据挖掘模型只是元数据属性的组合。 这些属性指定挖掘结构，指定数据挖掘算法，并定义影响如何处理数据的参数和筛选器设置的集合。 有关详细信息，请参阅[挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)。  
  
 处理模型时，存储在挖掘结构缓存中的定型数据用于基于数据的统计属性和算法及其参数定义的试探方法生成模式。 这称为“定型  ”模型。  
  
 定型的结果是一组汇总数据，包含在“模型内容” 中，它描述找到的模式并提供生成预测的规则。 有关详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
 在有限事例中，还可以将模型的逻辑结构导出到一个文件，该文件根据标准格式（预测建模标记语言 PMML）表示模型公式和数据绑定。 可以将此逻辑结构导入其他使用 PMML 的系统，然后所述的模型就可以用于预测了。 有关详细信息，请参阅 [了解 DMX Select 语句](../../dmx/understanding-the-dmx-select-statement.md)。  
  
  
##  <a name="bkmk_CustomObjects"></a> 自定义数据挖掘对象  
 可以在数据挖掘项目的上下文中使用的其他对象（如准确性图表或预测查询）不在解决方案内持久化，但是可以使用 ASSL 编写脚本或使用 AMO 生成。  
  
 此外，您可以通过添加这些自定义对象扩展 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上可用的服务和功能：  
  
 **自定义程序集**  
 可以使用符合 CLR 或 COM 标准的语言定义 .NET 程序集，然后注册到 SQL Server 实例。 程序集文件可从应用程序定义的位置加载，并且其副本将和数据一起保存到服务器中。 程序集文件的副本可用于在每次启动服务时加载程序集。  
  
 有关详细信息，请参阅 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)。  
  
 **自定义存储过程**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘支持使用存储过程来处理数据挖掘对象。 您可以创建自己的存储过程来扩展功能，以便更方便地使用预测查询和内容查询返回的数据。  
  
 [定义存储的过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 支持将下面的存储过程用于交叉验证中。  
  
 [数据挖掘存储过程（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)  
  
 此外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含很多供数据挖掘内部使用的系统存储过程。 尽管系统存储过程供内部使用，但是您可能发现它们是有用的快捷方式。 Microsoft 保留根据需要更改这些存储过程的权利；因此，对于生产而言，我们建议您使用 DMX、AMO 或 XMLA 创建查询。  
  
 **自定义插件算法**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 有关创建自己的算法，以及作为新数据挖掘服务的算法然后添加到的服务器实例中提供的机制。  
  
 Analysis Services 使用 COM 接口与插件算法进行通信。 若要了解有关如何实现新算法的详细信息，请参阅 [Plugin Algorithms](../../analysis-services/data-mining/plugin-algorithms.md)。  
  
 必须注册每个新算法，之后才能使用它。 为了注册某个算法，您将算法所需的元数据添加到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的 .ini 文件中。 必须将该信息添加到要计划使用新算法的每个实例。 添加算法后，可以重新启动实例，使用 MINING_SERVICES 架构行集来查看新算法，包括算法支持的选项和提供程序。  
  
  
## <a name="see-also"></a>另请参阅  
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [数据挖掘扩展插件 & #40; DMX & #41;引用](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
