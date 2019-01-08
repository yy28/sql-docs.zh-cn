---
title: 处理要求和注意事项 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], objects
- mining structures [Analysis Services], processing
- mining models [Analysis Services], processing
ms.assetid: f7331261-6f1c-4986-b2c7-740f4b92ca44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 181e2a367f6196d50f90aee77ca9590f55ba0ce4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369719"
---
# <a name="processing-requirements-and-considerations-data-mining"></a>处理要求和注意事项（数据挖掘）
  本主题介绍了一些处理数据挖掘对象时要记住的技术注意事项。 有关处理的涵义以及如何将处理应用于数据挖掘的一般说明，请参阅 [处理数据挖掘对象](processing-data-mining-objects.md)。  
  
 [针对关系存储区的查询](#bkmk_QueryReqs)  
  
 [处理挖掘结构](#bkmk_ProcessStructures)  
  
 [处理挖掘模型](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> 处理期间针对关系存储区的查询  
 对于数据挖掘，有以下三个处理阶段：查询源数据、确定原始统计信息和使用模型定义与算法对挖掘模型进行定型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器向提供原始数据的数据库发出查询。 此数据库可能是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 SQL Server 数据库引擎早期版本的实例。 处理数据挖掘结构时，源中的数据传输到挖掘结构，并在磁盘上保存为一种新的压缩格式。 并不会处理数据源中的每个列，而仅会处理绑定所定义的挖掘结构中包含的列。  
  
 使用此数据， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 生成所有数据和离散化列的索引，并对连续列创建单独索引。 针对每个嵌套表发出一个查询以创建索引，并根据每个嵌套表生成一个额外查询，以处理每对嵌套表和事例表之间的关系。 创建多个查询的原因在于处理特殊的内部多维数据存储区。 您可以通过设置服务器属性 `DatabaseConnectionPoolMax` 来限制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 发送到关系存储区的查询数。 有关详细信息，请参阅 [OLAP Properties](../server-properties/olap-properties.md)。  
  
 处理模型时，模型不会从数据源中重新读取数据，而从挖掘结构获取数据摘要。 服务器将使用创建的多维数据集以及缓存的索引和事例数据来创建独立的线程，以便为模型定型。  
  
 有关版本的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的支持并行模型处理，请参阅[SQL Server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473)。  
  
##  <a name="bkmk_ProcessStructures"></a> 处理挖掘结构  
 可以一起处理所有相关模型的挖掘结构，也可以单独进行处理。 在预期某些模型要用较长时间进行处理并且您想要延迟该操作时，从各模型单独处理挖掘结构可能会很有用。  
  
 有关详细信息，请参阅 [Process a Mining Structure](process-a-mining-structure.md)。  
  
 如果您十分关注对硬盘空间的节省，则请注意 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将挖掘结构缓存保留在本地。 也就是说，所有定型数据都将写在本地硬盘上。 如果您不希望缓存数据，则可以将挖掘结构的 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性设置为 `ClearAfterProcessing`，从而更改默认值。 这会在处理模型之后破坏缓存；但是，这还会在挖掘结构中禁用钻取功能。 有关详细信息，请参阅 [钻取查询（数据挖掘）](drillthrough-queries-data-mining.md)。  
  
 此外，如果您清理了缓存，则将无法使用维持测试集；如果已定义一个维持测试集，则此测试集分区的定义也将丢失。 有关维持测试集的详细信息，请参阅 [定型和测试数据集](training-and-testing-data-sets.md)。  
  
##  <a name="bkmk_ProcessModels"></a> 处理挖掘模型  
 您可以独立于其关联的挖掘结构来处理挖掘模型，也可以与该结构一起处理基于该结构的所有模型。  
  
 有关详细信息，请参阅 [处理挖掘模型](process-a-mining-model.md)。  
  
 但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，不能选择多个要与结构一起处理的挖掘模型。 如果您需要控制所处理的模型，则必须单独选择这些模型，或者使用 XMLA 或 DMX 连续处理多个模型。  
  
## <a name="when-reprocessing-is-required"></a>在需要重新处理时  
 在开始用定义的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模型进行工作之前，必须对其进行处理。 无论何时更改挖掘模型结构、更新定型数据、更改现有挖掘模型或在结构中添加挖掘模型，都必须重新处理挖掘模型。  
  
 在以下方案中也处理挖掘模型：  
  
 **部署项目**:具体取决于项目设置和项目的当前状态，在项目中的挖掘模型时通常处理完全部署该项目。  
  
 启动部署时处理即自动开始，除非 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上有以前处理过的版本且没有发生结构更改。 可以通过选中下拉列表中的“部署解决方案”或按 F5 键来部署项目。 您可以  
  
 有关如何设置控制挖掘模型部署方式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署属性的详细信息，请参阅 [部署数据挖掘解决方案](deployment-of-data-mining-solutions.md)。  
  
 **移动挖掘模型**:当通过使用 EXPORT 命令移动挖掘模型时，只有模型的定义导出的这包括需要向模型提供数据挖掘结构的名称。  
  
 针对以下方案使用 EXPORT 和 IMPORT 命令进行重新处理的要求：  
  
-   挖掘结构在目标实例上存在，并且挖掘结构处于未处理状态。  
  
     必须重新处理结构和模型。  
  
-   挖掘结构在目标实例上存在，并且挖掘结构已处理。 仅导出了挖掘模型。  
  
     可以不进行处理便使用模型。  
  
-   还通过使用 WITH DEENDENCIES 关键字导出了挖掘模型定义。  
  
     必须重新处理结构和模型。  
  
 有关详细信息，请参阅 [导出和导入数据挖掘对象](export-and-import-data-mining-objects.md)。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构 &#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [挖掘结构 &#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [多维模型对象处理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
