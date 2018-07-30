---
title: 使用 Analysis Services 中的 XMLA 开发 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a7af006d5d52002480844b8776d8262fa8ae202
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024644"
---
# <a name="developing-with-xmla-in-analysis-services"></a>在 Analysis Services 中使用 XMLA 开发
  XML for Analysis (XMLA) 是一种基于 SOAP 的 XML 协议，它专门设计用于可通过 HTTP 连接访问的任何标准多维数据源的通用数据访问。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用 XMLA 作为与客户端应用程序通信的唯一协议。 从根本上说，Analysis Services 支持的所有客户端库都可以采用 XMLA 来表示请求和响应。  
  
 作为开发人员，您可以使用 XMLA 将客户端应用程序与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 集成，而不必依赖 .NET Framework 或 COM 接口。 通过使用 XMLA 并与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立 HTTP 连接，可以满足包括在众多平台上托管在内的应用程序要求。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不仅完全符合 XMLA 1.1 规范，还对其进行了扩展，可支持数据定义、数据操作和数据控制。 Analysis Services 扩展被称为 Analysis Services 脚本语言 (ASSL)。 将 XMLA 与 ASSL 一起使用可支持比 XMLA 单独提供的功能更广泛的功能。 ASSL 有关的详细信息，请参阅[使用 Analysis Services 脚本语言进行开发&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[管理连接和会话&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|介绍如何连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，以及如何在 XMLA 中管理会话和有状态性。|  
|[处理错误和警告&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|介绍 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如何在 XMLA 中返回方法和命令的错误和警告信息。|  
|[定义和标识对象&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|介绍对象标识符和对象引用，以及如何在 XMLA 命令中使用标识符和引用。|  
|[管理事务&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|详细介绍如何使用[BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)命令来显式定义和管理当前 XMLA 上的事务会话。|  
|[取消命令&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|介绍如何使用[取消](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)命令来取消命令、 会话和 XMLA 中的连接。|  
|[执行批处理操作&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|介绍如何使用[批处理](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)要运行多个 XMLA 命令的命令，以串行或并行，同一事务中或作为单独的事务处理，使用的单个 XMLA[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)方法。|  
|[创建和更改对象&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|介绍如何使用[创建](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)， [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，和[删除](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)命令，以及 Analysis Services 脚本语言 (ASSL) 元素，以定义，更改或删除从对象[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。|  
|[锁定和解锁数据库&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|详细介绍如何使用[锁](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)和[解锁](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)用于锁定和解锁的命令[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。|  
|[处理对象 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|介绍如何使用[过程](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令到进程[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象。|  
|[合并分区&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|介绍如何使用[MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)命令要将分区合并在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。|  
|[设计聚合&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|介绍如何使用[DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)命令，在迭代或批处理模式下中的聚合设计的设计聚合到[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|  
|[备份、 还原和同步数据库 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|介绍如何使用[备份](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)和[还原](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令以备份和还原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]从备份文件的数据库。<br /><br /> 此外介绍了如何使用[同步](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令以使同步[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用现有的数据库的同一个实例或另一个实例的数据库。|  
|[插入、 更新和删除成员&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|介绍如何使用[插入](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，和[删除](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令将添加，更改或删除从允许写维度的成员。|  
|[正在更新单元格&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|介绍如何使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令以更改写入的分区中的单元格的值。|  
|[管理缓存&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|详细介绍如何使用[ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)命令来清除缓存的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象。|  
|[监视跟踪&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|介绍如何使用[订阅](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)命令以订阅并监视现有跟踪上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。|  
  
## <a name="data-mining-with-xmla"></a>使用 XMLA 进行数据挖掘  
 XML for Analysis 完全支持数据挖掘架构行集。 这些行集提供用于查询数据挖掘模型使用的信息[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)方法。 有关数据挖掘架构行集的详细信息，请参阅[数据挖掘架构行集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 有关 DMX 的详细信息，请参阅[数据挖掘扩展插件&#40;DMX&#41;引用](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
## <a name="namespace-and-schema"></a>命名空间和架构  
  
### <a name="namespace"></a>命名空间  
 此规范中定义的架构使用的 XML 命名空间`http://schemas.microsoft.com/AnalysisServices/2003/Engine`和标准缩写"DDL。"  
  
### <a name="schema"></a>架构  
 用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象定义语言的 XML 架构定义语言 (XSD) 架构的定义基于本节中架构元素和层次结构的定义。  
  
## <a name="extensibility"></a>扩展性  
 通过提供的对象定义语言架构的扩展性**批注**的所有对象包含的元素。 此元素可包含任何 XML 命名空间（定义 DDL 的目标命名空间除外）中的任何有效的 XML，但应遵守以下规则：  
  
-   XML 只能包含元素。  
  
-   每个元素都必须有唯一的名称。 建议的值**名称**引用的目标命名空间。  
  
 施加这些规则，以便内容**批注**可作为一组名称/值对通过决策支持对象 (DSO) 9.0 公开标记。  
  
 注释和内的空白**批注**并未包括具有子元素的标记可能不会保留。 此外，所有元素必须可读写；只读元素会被忽略。  
  
 会关闭对象定义语言架构，原因是服务器不允许替换架构中定义的元素的派生类型。 因此，服务器仅接受此处定义的元素集，不接受任何其他元素或属性。 未知的元素会导致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎引发错误。  
  
## <a name="see-also"></a>另请参阅  
 [开发使用 Analysis Services 脚本语言&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [了解 Microsoft OLAP 体系结构](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
