---
title: 在 Analysis Services 中通过 XMLA 进行开发 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2f5455b71306b3dd75406f107e5c1e971f6b923b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544999"
---
# <a name="developing-with-xmla-in-analysis-services"></a>在 Analysis Services 中使用 XMLA 开发
  XML for Analysis (XMLA) 是一种基于 SOAP 的 XML 协议，它专门设计用于可通过 HTTP 连接访问的任何标准多维数据源的通用数据访问。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用 XMLA 作为与客户端应用程序通信的唯一协议。 从根本上说，Analysis Services 支持的所有客户端库都可以采用 XMLA 来表示请求和响应。  
  
 作为开发人员，您可以使用 XMLA 将客户端应用程序与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 集成，而不必依赖 .NET Framework 或 COM 接口。 通过使用 XMLA 并与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立 HTTP 连接，可以满足包括在众多平台上托管在内的应用程序要求。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不仅完全符合 XMLA 1.1 规范，还对其进行了扩展，可支持数据定义、数据操作和数据控制。 Analysis Services 扩展被称为 Analysis Services 脚本语言 (ASSL)。 将 XMLA 与 ASSL 一起使用可支持比 XMLA 单独提供的功能更广泛的功能。 有关 ASSL 的详细信息，请参阅[&#40;ASSL&#41;Analysis Services 脚本编写语言进行开发](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[管理连接和会话 (XMLA)](managing-connections-and-sessions-xmla.md)|介绍如何连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，以及如何在 XMLA 中管理会话和有状态性。|  
|[&#41;XMLA &#40;处理错误和警告](handling-errors-and-warnings-xmla.md)|介绍 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如何在 XMLA 中返回方法和命令的错误和警告信息。|  
|[&#40;XMLA 定义和标识对象&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|介绍对象标识符和对象引用，以及如何在 XMLA 命令中使用标识符和引用。|  
|[&#40;XMLA&#41;管理事务](managing-transactions-xmla.md)|详细说明如何使用[BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)、 [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)和[RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla)命令在当前 XMLA 会话上显式定义和管理事务。|  
|[&#41;XMLA &#40;取消命令](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|介绍如何使用[cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)命令取消 XMLA 中的命令、会话和连接。|  
|[&#40;XMLA&#41;执行批处理操作](performing-batch-operations-xmla.md)|介绍如何使用[Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令以串行或并行方式在同一事务中或使用单个 xmla [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法运行多个 xmla 命令。|  
|[&#40;XMLA&#41;创建和更改对象](creating-and-altering-objects-xmla.md)|描述如何使用[Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)、 [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)和[Delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)命令以及 Analysis Services 脚本语言（ASSL）元素来定义、更改或删除实例中的对象 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。|  
|[&#40;XMLA&#41;锁定和解锁数据库](locking-and-unlocking-databases-xmla.md)|详细说明如何使用[lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)和[unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)命令锁定和解锁 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。|  
|[处理对象 (XMLA)](processing-objects-xmla.md)|介绍如何使用[process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)命令处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。|  
|[&#40;XMLA&#41;合并分区](merging-partitions-xmla.md)|介绍如何使用[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令合并实例上的分区 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。|  
|[&#40;XMLA&#41;设计聚合](designing-aggregations-xmla.md)|介绍如何使用迭代或批处理模式下的[DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla)命令在中设计聚合设计的聚合 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。|  
|[备份、还原和同步数据库 (XMLA)](backing-up-restoring-and-synchronizing-databases-xmla.md)|描述如何使用[备份](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)和[还原](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)命令来备份和还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 备份文件中的数据库。<br /><br /> 还介绍了如何使用[synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)命令将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库与同一实例或不同实例上的现有数据库同步。|  
|[&#40;XMLA 中插入、更新和删除成员&#41;](inserting-updating-and-dropping-members-xmla.md)|介绍如何使用[Insert](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)、 [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)和[Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)命令添加、更改或删除启用了写操作的维度中的成员。|  
|[&#40;XMLA&#41;更新单元](updating-cells-xmla.md)|介绍如何使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改启用了写操作的分区中的单元值。|  
|[&#40;XMLA 中管理缓存&#41;](managing-caches-xmla.md)|详细说明如何使用[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)命令清除对象的缓存 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。|  
|[监视跟踪 &#40;XMLA&#41;](monitoring-traces-xmla.md)|介绍如何使用 "[订阅](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla)" 命令订阅和监视实例上的现有跟踪 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。|  
  
## <a name="data-mining-with-xmla"></a>使用 XMLA 进行数据挖掘  
 XML for Analysis 完全支持数据挖掘架构行集。 这些行集提供使用[发现](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法查询数据挖掘模型的信息。 有关数据挖掘架构行集的详细信息，请参阅[数据挖掘架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 有关 DMX 的详细信息，请参阅[数据挖掘扩展 &#40;DMX&#41; 参考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
## <a name="namespace-and-schema"></a>命名空间和架构  
  
### <a name="namespace"></a>命名空间  
 在此规范中定义的架构使用 XML 命名空间 `https://schemas.microsoft.com/AnalysisServices/2003/Engine` 和标准缩写 "DDL"。  
  
### <a name="schema"></a>架构  
 用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象定义语言的 XML 架构定义语言 (XSD) 架构的定义基于本节中架构元素和层次结构的定义。  
  
## <a name="extensibility"></a>扩展性  
 可通过所有对象包含的 `Annotation` 元素提供对象定义语言架构的扩展性。 此元素可包含任何 XML 命名空间（定义 DDL 的目标命名空间除外）中的任何有效的 XML，但应遵守以下规则：  
  
-   XML 只能包含元素。  
  
-   每个元素都必须有唯一的名称。 建议 `Name` 的值引用目标命名空间。  
  
 采用这些规则以便 `Annotation` 标记的内容可通过决策支持对象 (DSO) 9.0 公开为一组名称/值对。  
  
 在 `Annotation` 标记内，不可保留未用子元素括起来的注释和空格。 此外，所有元素必须可读写；只读元素会被忽略。  
  
 会关闭对象定义语言架构，原因是服务器不允许替换架构中定义的元素的派生类型。 因此，服务器仅接受此处定义的元素集，不接受任何其他元素或属性。 未知的元素会导致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎引发错误。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言开发 &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [了解 Microsoft OLAP 体系结构](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
