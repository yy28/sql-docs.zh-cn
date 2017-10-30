---
title: "执行批处理操作 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e2673091cfba456834da77049036591e4591891
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="performing-batch-operations-xmla"></a>执行批处理操作 (XMLA)
  你可以使用[批处理](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)XML 用于 Analysis (XMLA) 若要运行多个 XMLA 命令使用的单个 XMLA 命令[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)方法。 你可以运行多个命令中包含**批处理**是作为单个事务或在为每个命令的单个事务、 以串行或并行命令。 你还可以指定的外部绑定和其他属性**批处理**命令处理多个[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>运行事务性和非事务性 Batch 命令  
 **批处理**命令在两种方式之一执行命令：  
  
 **事务性**  
 如果**事务**属性**批处理**命令设置为 true，**批处理**命令运行命令的所有包含的命令**批处理**命令在单个事务中 —*事务*批处理。  
  
 如果任何命令失败的事务性批处理中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在中回滚任何命令**批处理**以前失败的命令运行的命令和**批处理**命令立即结束。 中的任何命令**批处理**尚未运行的命令不会执行。 后**批处理**命令结束，**批处理**命令会报告遇到的失败的命令的任何错误。  
  
 **非事务性**  
 如果**事务**属性设置为 false，**批处理**命令运行所包含的每个命令**批处理**命令，在单独的事务- *非事务性*批处理。 如果任何命令失败到非事务性批处理中，**批处理**命令会继续运行之后失败的命令运行命令。 后**批处理**命令尝试运行所有命令，**批处理**命令包含，**批处理**命令报告发生的任何错误。  
  
 返回由命令中包含的所有结果**批处理**命令返回与命令包含在相同的顺序**批处理**命令。 返回的结果**批处理**命令取决于是否**批处理**命令是事务性还是非事务性。  
  
> [!NOTE]  
>  如果**批处理**命令包含不返回输出，如命令[锁](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)命令，并且该命令将成功运行，**批处理**命令将返回一个空[根](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)结果元素中的元素。 空**根**元素可确保每个命令中包含**批处理**命令可以与相应匹配**根**该命令的结果的元素。  
  
### <a name="returning-results-from-transactional-batch-results"></a>从事务性批处理结果返回结果  
 从事务性批处理中运行命令的结果不会返回之前整个**批处理**命令完成。 因为任何命令事务性批处理中的失败会导致整个运行的每个命令后，将不会返回结果**批处理**命令和所有包含的命令将被回滚。 如果所有命令将启动并成功运行，[返回](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)元素[ExecuteResponse](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)返回的元素**执行**方法**批处理**命令包含一个[结果](../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)元素，它又包含一个**根**为每个成功运行的命令中包含的元素**批处理**命令。 如果在任何命令**批处理**命令无法启动或无法完成，**执行**方法可以返回 SOAP 错误**批处理**包含的错误的命令失败的命令。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>从非事务性批处理结果返回结果  
 来自运行在非事务性批处理中的命令结果将返回在其中命令中包含的顺序**批处理**命令以及它们由每个命令返回。 如果没有中包含的命令**批处理**可以成功启动命令，**执行**方法返回包含有关错误的 SOAP 错误**批处理**命令。 如果至少一个命令已成功启动，**返回**元素**ExecuteResponse**返回的元素**执行**方法**批处理**命令包含一个**结果**元素，它又包含一个**根**为每个命令中包含的元素**批处理**命令. 如果在非事务性批处理中的一个或多个命令无法启动或无法完成，**根**该失败的命令的元素包含[错误](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)对错误进行描述的元素。  
  
> [!NOTE]  
>  只要可以启动非事务性批处理中的至少一个命令，非事务性批处理被视为已成功运行，即使在非事务性批处理中包含的每个命令的结果中返回错误**批处理**命令。  
  
## <a name="using-serial-and-parallel-execution"></a>使用串行和并行执行  
 你可以使用**批处理**要运行包含命令的命令以串行或并行。 下一个命令时将以串行方式运行命令，在中包含**批处理**命令中的当前正在运行命令之前无法启动**批处理**命令完成。 时以并行方式运行命令，可以通过同时执行多个命令**批处理**命令。  
  
 若要并行运行命令，你添加命令以运行以并行方式对[并行](../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)属性**批处理**命令。 目前，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以仅运行，连续、 顺序[过程](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)并行中的命令。 任何其他 XMLA 命令，如[创建](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)或[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)、 包含在**并行**属性按顺序运行。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]尝试运行所有**过程**命令包含在**并行**属性并行，但不能保证，包括所有**过程**可以并行运行命令。 实例分析上述各**过程**命令和实例确定，该命令不能并行运行的如果**过程**命令以串行方式运行。  
  
> [!NOTE]  
>  若要并行运行命令**事务**属性**批处理**命令必须设置为 true，因为[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支持每个连接和非事务性只有一个活动事务在单独的事务中运行每个命令的批次。 如果包含**并行**非事务性批处理中的属性，就会出错。  
  
### <a name="limiting-parallel-execution"></a>限制并行执行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例尝试运行任意多个**过程**尽可能情况下，直到达到实例运行的计算机的限制的并行命令。 可以限制的同时执行数目**过程**通过设置命令**maxParallel**属性**并行**到一个值，该值的属性最大数目**过程**可以并行运行的命令。  
  
 例如，**并行**属性包含按照列出的顺序中的以下命令：  
  
1.  **创建**  
  
2.  **处理**  
  
3.  **Alter**  
  
4.  **处理**  
  
5.  **处理**  
  
6.  **处理**  
  
7.  **删除**  
  
8.  **处理**  
  
9. **处理**  
  
 **MaxParalle**l 属性**并行**属性设置为 2。 因此，实例按照以下列表中所述，运行前面列表中的命令：  
  
-   1 命令按顺序运行，因为命令 1**创建**命令，并且只**过程**可以并行运行命令。  
  
-   完成命令 1 后，按顺序运行命令 2。  
  
-   完成命令 2 后，按顺序运行命令 3。  
  
-   完成命令 3 后，命令 4 和 5 中并行运行。 虽然命令 6 也是但是**过程**命令时，命令 6 无法与命令 4 和 5 并行运行，因为**maxParallel**属性设置为 2。  
  
-   命令 6 以串行方式在命令 4 和 5 都完成后运行。  
  
-   命令 7 以串行方式在命令 6 完成后运行。  
  
-   命令 8 和 9 以并行方式在命令 7 完成后运行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令处理对象  
 **批处理**命令包含几个可选的属性和专门包含以支持的属性处理多个[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目：  
  
-   **ProcessAffectedObjects**属性**批处理**命令指示实例是否应还处理需要重新处理引发的任何对象**过程**命令包含在**批处理**命令处理指定的对象。  
  
-   [绑定](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)属性包含的外部绑定使用的所有集合**过程**中的命令**批处理**命令。  
  
-   [数据源](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)属性包含使用的所有数据源的外部绑定**过程**中的命令**批处理**命令。  
  
-   [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)属性包含的所有用户使用的数据源视图的外部绑定**过程**中的命令**批处理**命令。  
  
-   [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md)属性指定的方式在其中**批处理**命令处理遇到的所有错误**过程**中包含的命令**批处理**命令。  
  
    > [!IMPORTANT]  
    >  A**过程**命令不能包括**绑定**，**数据源**， **DataSourceView**，或**ErrorConfiguration**属性，如果**过程**命令包含在**批处理**命令。 如果你必须指定这些属性**过程**命令中，提供所需信息的对应属性中**批处理**命令包含**过程**命令。  
  
## <a name="see-also"></a>另请参阅  
 [Batch 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Process 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

