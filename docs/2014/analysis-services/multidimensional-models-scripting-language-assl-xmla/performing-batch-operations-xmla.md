---
title: 执行批处理操作 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7f164ca12c1de105bcd73f9b371ff4bfe2e00182
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015345"
---
# <a name="performing-batch-operations-xmla"></a>执行批处理操作 (XMLA)
  你可以使用[批处理](../xmla/xml-elements-commands/batch-element-xmla.md)XML 用于 Analysis (XMLA) 若要运行多个 XMLA 命令使用的单个 XMLA 命令[执行](../xmla/xml-elements-methods-execute.md)方法。 可以作为单个事务或者每个命令为一个事务，以串行或并行方式运行 `Batch` 命令中包含的多个命令。 你还可以指定的外部绑定和其他属性`Batch`命令处理多个[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>运行事务性和非事务性 Batch 命令  
 `Batch` 以下列两种方式之一执行命令：  
  
 **事务性**  
 如果`Transaction`属性`Batch`命令设置为 true，`Batch`命令运行命令的所有包含的命令`Batch`命令在单个事务中 —*事务*批处理。  
  
 如果任何命令失败的事务性批处理中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在中回滚任何命令`Batch`以前失败的命令运行的命令和`Batch`命令立即结束。 `Batch` 命令中尚未运行的任何命令都不再执行。 `Batch` 命令结束后，`Batch` 命令将报告失败命令发生的所有错误。  
  
 **非事务性**  
 如果`Transaction`属性设置为 false，`Batch`命令运行所包含的每个命令`Batch`命令，在单独的事务-*非事务性*批处理。 如果非事务性批处理中的任一命令失败，`Batch` 命令会继续执行失败命令后的命令。 `Batch` 命令尝试运行 `Batch` 命令包含的所有命令后，`Batch` 命令将报告发生的所有错误。  
  
 `Batch` 命令中包含的各命令返回的所有结果以这些命令包含在 `Batch` 命令中的顺序返回。 `Batch` 命令返回的结果根据 `Batch` 命令是事务性的还是非事务性的而不同。  
  
> [!NOTE]  
>  如果`Batch`命令包含不返回输出，如命令[锁](../xmla/xml-elements-commands/lock-element-xmla.md)命令，并且该命令将成功运行，`Batch`命令将返回一个空[根](../xmla/xml-elements-properties/root-element-xmla.md)元素中的结果元素中。 空的 `root` 元素可确保 `Batch` 命令中包含的每个命令都与该命令的结果的相应 `root` 元素匹配。  
  
### <a name="returning-results-from-transactional-batch-results"></a>从事务性批处理结果返回结果  
 只有在整个 `Batch` 命令全部完成之后，才会从事务性批处理中运行的命令返回结果。 由于事务性批处理中任一命令失败将导致整个 `Batch` 命令及其包含的所有命令都回滚，因此不在每个命令运行后返回结果。 如果所有命令将启动并成功运行，[返回](../xmla/xml-elements-properties/return-element-xmla.md)元素[ExecuteResponse](../xmla/xml-elements-objects-executeresponse.md)返回的元素`Execute`方法`Batch`命令包含一个[结果](../xmla/xml-elements-properties/results-element-xmla.md)元素，它又包含一个`root`为每个成功运行的命令中包含的元素`Batch`命令。 如果 `Batch` 命令中的任一命令无法启动或完成，`Execute` 方法将为 `Batch` 命令返回一个 SOAP 错误，其中包含失败命令的错误。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>从非事务性批处理结果返回结果  
 从非事务性批处理中运行的命令返回的结果以这些命令在 `Batch` 命令中的顺序返回，并且在每个命令返回结果时即将该结果返回。 如果 `Batch` 命令中包含的命令都无法成功启动，`Execute` 方法将返回包含 `Batch` 命令的错误的 SOAP 错误。 如果至少一个命令成功启动，则由 `return` 命令的 `ExecuteResponse` 方法返回的 `Execute` 元素的 `Batch` 元素将包含一个 `results` 元素，该元素为 `root` 命令中包含的每个命令包含一个 `Batch` 元素。 如果在非事务性批处理中的一个或多个命令无法启动或无法完成，`root`该失败的命令的元素包含[错误](../xmla/xml-elements-properties/error-element-xmla.md)对错误进行描述的元素。  
  
> [!NOTE]  
>  只要非事务性批处理中至少有一个命令能够启动，就认为该非事务性批处理成功运行，即使该非事务性批处理中包含的每个命令都在 `Batch` 命令的结果中返回错误。  
  
## <a name="using-serial-and-parallel-execution"></a>使用串行和并行执行  
 可以使用 `Batch` 命令以串行或并行方式运行所包含的命令。 以串行方式运行命令时，`Batch` 命令中包含的下一个命令必须等 `Batch` 命令中当前运行的命令完成后才能启动。 以并行方式运行命令时，`Batch` 命令可以同时执行多个命令。  
  
 若要并行运行命令，你添加命令以运行以并行方式对[并行](../xmla/xml-elements-properties/parallel-element-xmla.md)属性`Batch`命令。 目前，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以仅运行，连续、 顺序[过程](../xmla/xml-elements-commands/process-element-xmla.md)并行中的命令。 任何其他 XMLA 命令，如[创建](../xmla/xml-elements-commands/create-element-xmla.md)或[Alter](../xmla/xml-elements-commands/alter-element-xmla.md)、 包含在`Parallel`属性按顺序运行。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 尝试以并行方式运行包含在 `Process` 属性中的所有 `Parallel` 命令，但是不保证包含的所有 `Process` 命令都能以并行方式运行。 实例会分析每个 `Process` 命令，如果实例确定命令不能以并行方式执行，则 `Process` 命令将以串行方式执行。  
  
> [!NOTE]  
>  若要以并行方式执行命令，`Transaction` 命令的 `Batch` 属性必须设置为 true，因为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅支持每个连接一个活动事务且非事务性批处理在单独的事务中执行每个命令。 如果在非事务性批处理中包含 `Parallel` 属性，则将出现错误。  
  
### <a name="limiting-parallel-execution"></a>限制并行执行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例并行运行尽可能多的 `Process` 命令，直到达到运行实例的计算机的限制。 将 `Process` 属性的 `maxParallel` 特性设为指示可并发执行的最大 `Parallel` 命令数，可限制同时执行的 `Process` 命令数。  
  
 例如，`Parallel` 属性按列出的顺序包含以下命令：  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 此 `maxParalle` 属性的 `Parallel`l 特性设置为 2。 因此，实例按照以下列表中所述，运行前面列表中的命令：  
  
-   命令 1 以串行方式运行，因为命令 1 是 `Create` 命令，而只有 `Process` 命令能以并行方式运行。  
  
-   完成命令 1 后，按顺序运行命令 2。  
  
-   完成命令 2 后，按顺序运行命令 3。  
  
-   完成命令 3 后，命令 4 和 5 中并行运行。 虽然命令 6 也是 `Process` 命令，但是命令 6 不能与命令 4 和 5 并行运行，因为 `maxParallel` 属性设置为 2。  
  
-   命令 6 以串行方式在命令 4 和 5 都完成后运行。  
  
-   命令 7 以串行方式在命令 6 完成后运行。  
  
-   命令 8 和 9 以并行方式在命令 7 完成后运行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令处理对象  
 `Batch` 命令包含多个专门用于支持处理多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的可选属性和特性：  
  
-   `ProcessAffectedObjects` 命令的 `Batch` 特性指示实例是否还应对作为 `Process` 命令中包含的处理特定对象的 `Batch` 命令的结果而需要重新处理的所有对象进行处理。  
  
-   [绑定](../xmla/xml-elements-properties/bindings-element-xmla.md)属性包含的外部绑定使用的所有集合`Process`中的命令`Batch`命令。  
  
-   [数据源](../xmla/xml-elements-properties/source-element-xmla.md)属性包含使用的所有数据源的外部绑定`Process`中的命令`Batch`命令。  
  
-   [DataSourceView](../xmla/xml-elements-properties/datasourceview-element-xmla.md)属性包含的所有用户使用的数据源视图的外部绑定`Process`中的命令`Batch`命令。  
  
-   [ErrorConfiguration](../xmla/xml-elements-properties/errorconfiguration-element-xmla.md)属性指定的方式在其中`Batch`命令处理遇到的所有错误`Process`命令中包含`Batch`命令。  
  
    > [!IMPORTANT]  
    >  如果 `Process` 命令包含在 `Bindings` 命令中，则 `DataSource` 命令不能包含 `DataSourceView`、`ErrorConfiguration`、`Process` 或 `Batch` 属性。 如果必须为 `Process` 命令指定这些属性，请在包含 `Batch` 命令的 `Process` 命令的相应属性中提供必要的信息。  
  
## <a name="see-also"></a>请参阅  
 [批处理元素&#40;XMLA&#41;](../xmla/xml-elements-commands/batch-element-xmla.md)   
 [处理元素&#40;XMLA&#41;](../xmla/xml-elements-commands/process-element-xmla.md)   
 [多维模型对象处理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  