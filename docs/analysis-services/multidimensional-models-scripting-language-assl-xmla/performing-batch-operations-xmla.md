---
title: 执行批处理操作 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544232"
---
# <a name="performing-batch-operations-xmla"></a>执行批处理操作 (XMLA)
  可以使用[批处理](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，在 XML for Analysis (XMLA) 运行多个 XMLA 命令，使用单个 XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法。 你可以运行多个命令中包含**批处理**作为单个事务或在每个命令的单个事务中，以串行或并行命令。 您还可以指定的外部绑定和其他属性**批处理**命令用于处理多个[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>运行事务性和非事务性 Batch 命令  
 **批处理**命令在两种方式之一执行命令：  
  
 **事务性**  
 如果**事务**的属性**批处理**命令设置为 true 时，**批处理**命令运行命令的所有命令所包含的**批处理**命令在单个事务 a*事务性*批处理。  
  
 如果事务性批处理中任一命令失败[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回滚任何命令**批处理**失败命令之前运行的命令和**批处理**命令立即结束。 中的任何命令**批处理**尚未运行的命令不会执行。 之后**批处理**命令结束，**批处理**命令会报告失败命令发生的任何错误。  
  
 **非事务性**  
 如果**事务**属性设置为 false， **Batch**命令运行所包含的每个命令**批处理**命令，在单独的事务的*非事务性*批处理。 如果非事务性批处理中任一命令失败**批处理**命令会继续运行后失败的命令运行命令。 之后**批处理**命令尝试运行所有命令的**Batch**命令包含时，**批处理**命令报告发生任何错误。  
  
 返回命令中包含的所有结果**批处理**命令返回在其中命令中包含的相同顺序**批处理**命令。 返回的结果**批处理**命令因是否**批处理**命令是事务性还是非事务性。  
  
> [!NOTE]  
>  如果**批处理**命令包含不返回输出，如命令[锁](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)命令，并该命令成功运行，**批处理**命令将返回一个空[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)结果元素中的元素。 空**根**元素可确保每个命令中包含**Batch**命令可以与相应匹配**根**该命令的结果的元素。  
  
### <a name="returning-results-from-transactional-batch-results"></a>从事务性批处理结果返回结果  
 从事务性批处理中运行的命令的结果不会返回直到整个**批处理**命令完成。 结果不会返回后运行每个命令，因为任何命令事务性批处理中的失败将导致整个**批处理**命令，并回滚包含的所有命令。 如果所有命令开始并成功运行，则[返回](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla)的元素[ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse)返回元素**Execute**方法**批处理**命令包含一个[结果](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla)元素，它又包含一个**根**元素中包含的每个成功运行命令**批处理**命令。 如果中的任一命令**批处理**命令无法启动或无法完成， **Execute**方法返回的 SOAP 错误**批处理**包含的错误的命令失败的命令。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>从非事务性批处理结果返回结果  
 从非事务性批处理中运行的命令的结果返回在其中命令中包含的顺序**批处理**命令和它们返回的每个命令。 如果中包含的命令**批处理**命令可以成功启动， **Execute**方法将返回包含有关错误的 SOAP 错误**批处理**命令。 如果至少一个命令已成功启动，**返回**的元素**ExecuteResponse**返回元素**Execute**方法**批处理**命令包含一个**结果**元素，它又包含一个**根**元素中包含的每个命令**批处理**命令. 如果非事务性批处理中的一个或多个命令无法启动或无法完成，**根**失败命令的元素包含[错误](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)描述错误的元素。  
  
> [!NOTE]  
>  只要非事务性批处理中的至少一个命令可启动，非事务性批处理被视为已成功运行，即使在非事务性批处理中包含的每个命令的结果中返回一个错误**批处理**命令。  
  
## <a name="using-serial-and-parallel-execution"></a>使用串行和并行执行  
 可以使用**批处理**命令来运行所包含的命令以串行或并行。 在序列中运行命令下, 一个命令将包含在**批处理**命令中的当前正在运行命令才能启动**批处理**命令完成。 可以同时执行多个命令时以并行方式运行命令，**批处理**命令。  
  
 若要以并行方式运行命令，你添加到并行运行的命令[并行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla)的属性**批处理**命令。 目前，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以仅在运行连续的顺序[进程](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)并行中的命令。 任何其他 XMLA 命令，如[创建](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)或[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)，包含在**并行**属性以串行方式运行。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 尝试运行所有**进程**命令中包含**并行**并行情况下，属性但不能保证包含的所有**过程**可以并行运行命令。 该实例会分析每个**进程**命令和，如果实例确定不能并行运行命令**进程**在序列中运行命令。  
  
> [!NOTE]  
>  若要并行情况下，运行命令**事务**的属性**Batch**命令必须设置为 true，因为[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支持只有一个活动事务，每个连接和非事务性在一个单独的事务中运行每个命令的批次。 如果包括**并行**非事务性批处理中的属性，就会出错。  
  
### <a name="limiting-parallel-execution"></a>限制并行执行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例将尝试运行尽可能多**进程**尽可能，直到达到运行实例的计算机限制的并行中的命令。 可以限制的并发执行数**进程**通过设置命令**maxParallel**的属性**并行**属性设置为一个值，该值指示最大数**进程**可以并行运行的命令。  
  
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
  
 **MaxParalle**l 特性**并行**属性设置为 2。 因此，实例按照以下列表中所述，运行前面列表中的命令：  
  
-   因为命令 1 是按顺序运行命令 1**创建**命令，而只有**进程**可以并行运行命令。  
  
-   在命令 1 完成后，按顺序运行命令 2。  
  
-   在命令 2 完成后，按顺序运行命令 3。  
  
-   在命令 3 完成后，命令 4 和 5 并行运行。 虽然命令 6 也是**进程**命令，命令 6 不能与命令 4 和 5 并行运行，因为**maxParallel**属性设置为 2。  
  
-   命令 6 以串行方式在命令 4 和 5 都完成后运行。  
  
-   命令 7 以串行方式在命令 6 完成后运行。  
  
-   命令 8 和 9 以并行方式在命令 7 完成后运行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令处理对象  
 **批处理**命令包含多个可选属性和特性专门包含在内以支持处理多个[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目：  
  
-   **ProcessAffectedObjects**的属性**Batch**命令指示实例是否还应处理任何对象，而需要重新为**过程**命令中包含**批处理**命令处理指定的对象。  
  
-   [绑定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)属性包含的所有使用的外部绑定集合**进程**中的命令**批处理**命令。  
  
-   [数据源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla)属性包含的所有使用的数据源的外部绑定**进程**中的命令**批处理**命令。  
  
-   [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)属性包含的所有使用的数据源视图的外部绑定**进程**中的命令**批处理**命令。  
  
-   [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)属性中指定的方式**Batch**命令处理遇到的所有错误**过程**中所包含的命令**批处理**命令。  
  
    > [!IMPORTANT]  
    >  一个**进程**命令不能包含**绑定**，**数据源**， **DataSourceView**，或**ErrorConfiguration**属性，如果**进程**命令包含在**批处理**命令。 如果你必须指定这些属性**进程**命令，提供必要的信息的相应属性中**Batch**包含的命令**过程**命令。  
  
## <a name="see-also"></a>请参阅  
 [批处理元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [处理元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
