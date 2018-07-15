---
title: 线程池属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PriorityRatio property
- threads [Analysis Services]
- MinThreads property
- NumThreads property
- MaxThreads property
- Concurrency property
ms.assetid: e2697bb6-6d3f-4621-b9fd-575ac39c2185
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f19468e128b6009a19acd2ace84c99dc2e0140d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303027"
---
# <a name="thread-pool-properties"></a>线程池属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用多线程处理许多操作，通过并行运行多个作业提高总体服务器性能。 为了更高效地管理线程， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用线程池预分配线程并提高下一作业的线程可用性。  
  
 每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例都维持有自己的一组线程池。 表格实例和多维实例在使用线程池的方式上有着重大区别。 最重要的区别是在于只有多维解决方案使用`IOProcess`线程池。 在这种情况下，`PerNumaNode`属性，本主题中所述不是针对表格实例有意义。  
  
 本主题包含以下各节：  
  
-   [Analysis Services 中的线程管理](#bkmk_threadarch)  
  
-   [线程池属性参考](#bkmk_propref)  
  
-   [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity)  
  
-   [设置 PerNumaNode 以使 IO 线程与 NUMA 节点中的处理器关联](#bkmk_pernumanode)  
  
-   [确定当前线程池设置](#bkmk_currentsettings)  
  
-   [依赖或相关属性](#bkmk_related)  
  
-   [关于 MSMDSRV.INI](#bkmk_msmdrsrvini)  
  
> [!NOTE]  
>  NUMA 系统上的表格部署不在本主题讨论范围内。 虽然表格解决方案可以成功部署在 NUMA 系统上，但在高度纵向扩展的体系结构中，表格模型使用的内存中数据库技术的性能特性所展现出的优点可能有限。 有关详细信息，请参阅 [Analysis Services 案例研究：在大型商业解决方案中使用表格模型](http://msdn.microsoft.com/library/dn751533.aspx) 和 [调整表格解决方案大小的硬件](http://go.microsoft.com/fwlink/?LinkId=330359)。  
  
##  <a name="bkmk_threadarch"></a> Analysis Services 中的线程管理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用多线程通过增加并行执行的任务数来充分利用可用的 CPU 资源。 存储引擎是多线程的。 例如，在存储引擎内执行的多线程作业包括并行处理对象或处理已推送到存储引擎的离散查询，或返回查询所请求的数据值。 由于公式引擎计算的串行特性，它将进行单线程处理。 每个查询主要在单线程中执行，发出请求后往往需要等待存储引擎返回数据。 查询线程的执行时间较长，仅当整个查询完成后才会将其释放。  
  
 默认情况下，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本上， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用所有可用的逻辑处理器，在运行较高版本的 Windows 和 SQL Server 的系统上最多使用 640 个。 启动时，msmdsrv.exe 进程将分配给特定处理器组，但随着时间的推移，可在任何处理器组的任意逻辑处理器上对线程进行计划。  
  
 使用大量处理器的一个副作用是，有时候您可能会遇到性能降级情况，因为查询和处理负荷被分散在大量处理器上，对共享数据结构的争用将会加剧。 这种情况主要发生在采用 NUMA 体系结构的高端系统上，但在同一硬件上运行多个需要处理大量数据的应用程序的非 NUMA 系统上也会出现这种情况。  
  
 若要缓解此问题，您可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 操作类型和一组特定逻辑处理器之间设置关联。 使用 `GroupAffinity` 属性，您可以创建自定义关联掩码，以指定对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理的每个线程池类型使用哪种系统资源。  
  
 对于用于各种 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作负载的五个线程池，都可以设置自定义关联：  
  
-   **解析\短**  是用于短请求的解析池。 可纳入单一网络消息中的请求视为短请求。  
  
-   **解析\长**  是用于不可纳入单一网络消息中的所有其他请求的解析池。  
  
    > [!NOTE]  
    >  来自两种解析池的线程都可以用来执行查询。 诸如快速发现或取消请求等快速执行的查询有时会立即执行，而不是排队进入查询线程池。  
  
-   `Query` 线程池是用于执行由分析线程池未处理的所有请求。 此线程池中的线程将执行所有类型的操作，如发现、MDX、DAX、DMX 和 DDL 命令。  
  
-   `IOProcess` 用于与多维引擎中的存储引擎查询关联的 IO 作业。 这些线程所做的工作应该不依赖于其他线程。 这些线程通常将扫描单个分区段，并对段数据执行筛选和聚合操作。 `IOProcess` 线程通常对 NUMA 硬件配置特别敏感。 在这种情况下，此线程池具有`PerNumaNode`配置属性，可用于根据需要优化性能。  
  
-   `Process` 适用于较长的持续时间存储引擎作业，包括聚合、 索引和提交操作。 ROLAP 存储模式还使用“处理”线程池中的线程。  
  
> [!NOTE]  
>  虽然 Msmdsrv.ini 中具有线程池设置`VertiPaq`部分中， `VertiPaq` \\ `ThreadPool` \\ `GroupAffinity`并`ThreadPool` \\ `CPUs`刻意未作记录。 这些属性当前不起作用，保留供日后使用。  
  
 对于服务请求， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可能会超过最大线程池限制，必要时会请求额外线程来执行工作。 但是，当某一线程执行完自己的任务后，如果当前线程数超过最大限制，则该线程即会终止，而不是返回线程池。  
  
> [!NOTE]  
>  超出最大线程池计数是只有在出现某些死锁情况时才调用的保护。 为了避免超出该最大值的失控线程创建，应在达到了该最大限值后逐步创建线程（在短暂延迟后）。 超出该最大线程池计数可能会导致任务执行速度减慢。 如果性能计数器显示线程计数定期超出该线程池最大大小，则您可以考虑将其作为指示器，指示线程池大小对于要从系统请求的并发度而言太小。  
  
 默认情况下，线程池大小由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]确定并且基于内核数。 服务器启动后，您可以通过检查 msmdsrv.log 文件来观察选定的默认值。 作为一项性能调节练习，您可以选择增加线程池的大小以及其他属性，以此来提高查询或处理性能。  
  
##  <a name="bkmk_propref"></a> 线程池属性参考  
 本节介绍在每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的 msmdsrv.ini 文件中找到的线程池属性。 这些属性中的一部分也出现在 SQL Server Management Studio 中。  
  
 按字母顺序列出属性。  
  
|“属性”|类型|Description|默认|指导|  
|----------|----------|-----------------|-------------|--------------|  
|`IOProcess` \ `Concurrency`|double|一个双精度浮点值，确定用于设置可同时排队的线程数目标的算法。|2.0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 并发用于初始化线程池，这些线程池使用 Windows 中的 IO 完成端口来实施。 有关详细信息，请参阅 [I/O 完成端口](http://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `GroupAffinity`|string|一个十六进制值的数组，这些值与系统上的处理器组相对应，用于设置 IOProcess 线程池中的线程与每个处理器组中的逻辑处理器的关联。|none|可以使用此属性创建自定义关联。 该属性默认为空。<br /><br /> 有关详细信息，请参阅 [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity) 。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `MaxThreads`|ssNoversion|有符号 32 位整数，用于指定线程池中要包含的最大线程数。|0|0 指示由服务器确定默认值。 默认情况下，服务器将此值设置为 64 或设置为逻辑处理器数的 10 倍，以较大者为准。 例如，在采用超线程的 4 核系统上，线程池最大值是 80 个线程。<br /><br /> 如果将此值设置为负值，则服务器将该值乘以逻辑处理器数。 例如，当在具有 32 个逻辑处理器的服务器上设置为 -10 时，最大值是 320 个线程。<br /><br /> 最大值取决于按以前定义的任何自定义关联掩码可用的处理器数。 例如，如果您已将线程池关联设置为使用 32 个处理器中的 8 个，并且现在将 MaxThreads 设置为 -10，则线程池的上限将为 10 乘以 8（即 80 个线程）。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `MinThreads`|ssNoversion|一种 32 位有符号整数，用于指定为线程池预分配的最小线程数。|0|0 指示由服务器确定默认值。 默认情况下，最小值为 1。<br /><br /> 如果将此值设置为负值，服务器会将此值乘以逻辑处理器数。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `PerNumaNode`|ssNoversion|有符号 32 位整数，用于确定为 msmdsrv 进程创建的线程池数。|-1|有效值为 -1、0、1、2<br /><br /> -1 = 服务器根据 NUMA 节点数选择不同的 IO 线程池策略。 在 NUMA 节点数少于 4 个的系统上，服务器行为与值为 0 时的行为相同（为系统创建一个 IOProcess 线程池）。 在具有 4 个或更多个节点的系统中，行为与 1 相同（为每个节点创建 IOProcess 线程池）。<br /><br /> 0 = 禁用每节点 NUMA 多个线程池，以便 msmdsrv.exe 进程仅使用一个 IOProcess 线程池。<br /><br /> 1 = 为每个 NUMA 节点启用一个 IOProcess 线程池。<br /><br /> 2 = 每个逻辑处理器一个 IOProcess 线程池。 每个线程池中的线程数与逻辑处理器的 NUMA 节点关联，且理想处理器设置为逻辑处理器。<br /><br /> 有关详细信息，请参阅 [设置 PerNumaNode 以使 IO 线程与 NUMA 节点中的处理器关联](#bkmk_pernumanode) 。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `PriorityRatio`|ssNoversion|有符号 32 位整数，可用于确保即使高优先级队列不为空，有时也能执行低优先级线程。|2|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 仅适用于多维模型。|  
|`IOProcess` \ `StackSizeKB`|ssNoversion|一种 32 位有符号整数，可用于调整线程执行期间的内存分配。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 仅适用于多维模型。|  
|**分析**  \ `Long` \ `Concurrency`|double|一个双精度浮点值，确定用于设置可同时排队的线程数目标的算法。|2.0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 并发用于初始化线程池，这些线程池使用 Windows 中的 IO 完成端口来实施。 有关详细信息，请参阅 [I/O 完成端口](http://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|**分析**  \ `Long` \ `GroupAffinity`|string|一个十六进制值的数组，这些值与系统上的处理器组相对应，用于设置分析线程与每个处理器组中的逻辑处理器的关联。|none|可以使用此属性创建自定义关联。 该属性默认为空。<br /><br /> 有关详细信息，请参阅 [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity) 。|  
|**分析**  \ `Long` \ `NumThreads`|ssNoversion|有符号 32 位整数属性，用于定义可为长命令创建的线程数。|0|0 表示由服务器决定默认值。 默认行为是设置`NumThreads`为绝对值 4，或逻辑处理器数的 2 倍，大者为准。<br /><br /> 如果将此值设置为负值，则服务器将该值乘以逻辑处理器数。 例如，当在具有 32 个逻辑处理器的服务器上设置为 -10 时，最大值是 320 个线程。<br /><br /> 最大值取决于按以前定义的任何自定义关联掩码可用的处理器数。 例如，如果已将线程池关联设置为使用 32 个处理器中的 8 个，并且现在将 NumThreads 设置为 -10，则线程池的上限将为 10 乘以 8，即 80 个线程。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。|  
|**分析**  \ `Long` \ `PriorityRatio`|ssNoversion|一种 32 位有符号整数，可用于确保即使高优先级队列不为空，有时也可以执行低优先级线程。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|**分析**  \ `Long` \ `StackSizeKB`|ssNoversion|一种 32 位有符号整数，可用于调整线程执行期间的内存分配。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|**分析**  \ `Short` \ `Concurrency`|double|一个双精度浮点值，确定用于设置可同时排队的线程数目标的算法。|2.0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 并发用于初始化线程池，这些线程池使用 Windows 中的 IO 完成端口来实施。 有关详细信息，请参阅 [I/O 完成端口](http://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|**分析**  \ `Short` \ `GroupAffinity`|string|一个十六进制值的数组，这些值与系统上的处理器组相对应，用于设置分析线程与每个处理器组中的逻辑处理器的关联。|none|可以使用此属性创建自定义关联。 该属性默认为空。<br /><br /> 有关详细信息，请参阅 [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity) 。|  
|**分析**  \ `Short` \ `NumThreads`|ssNoversion|有符号 32 位整数属性，用于定义可为短命令创建的线程数。|0|0 表示由服务器决定默认值。 默认行为是设置`NumThreads`为绝对值 4，或逻辑处理器数的 2 倍，大者为准。<br /><br /> 如果将此值设置为负值，则服务器将该值乘以逻辑处理器数。 例如，当在具有 32 个逻辑处理器的服务器上设置为 -10 时，最大值是 320 个线程。<br /><br /> 最大值取决于按以前定义的任何自定义关联掩码可用的处理器数。 例如，如果已将线程池关联设置为使用 32 个处理器中的 8 个，并且现在将 NumThreads 设置为 -10，则线程池的上限将为 10 乘以 8，即 80 个线程。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。|  
|**分析**  \ `Short` \ `PriorityRatio`|ssNoversion|一种 32 位有符号整数，可用于确保即使高优先级队列不为空，有时也可以执行低优先级线程。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|**分析**  \ `Short` \ `StackSizeKB`|ssNoversion|有符号 32 位整数，可用于在线程执行期间调整内存分配。|64 * 逻辑处理器数|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|`Process` \ `Concurrency`|double|一个双精度浮点值，确定用于设置可同时排队的线程数目标的算法。|2.0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 并发用于初始化线程池，这些线程池使用 Windows 中的 IO 完成端口来实施。 有关详细信息，请参阅 [I/O 完成端口](http://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|`Process` \ `GroupAffinity`|string|一个十六进制值的数组，这些值与系统上的处理器组相对应，用于设置处理线程与每个处理器组中的逻辑处理器的关联。|none|可以使用此属性创建自定义关联。 该属性默认为空。<br /><br /> 有关详细信息，请参阅 [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity) 。|  
|`Process` \ `MaxThreads`|ssNoversion|有符号 32 位整数，用于指定线程池中要包含的最大线程数。|0|0 表示由服务器确定默认值。 默认情况下，服务器将此值设置为绝对值 64，或逻辑处理器数，取两者中的较大值。 例如，在启用超线程的 64 核系统上（一共 128 个逻辑处理器），线程池最大值是 128 个线程。<br /><br /> 如果将此值设置为负值，则服务器将该值乘以逻辑处理器数。 例如，当在具有 32 个逻辑处理器的服务器上设置为 -10 时，最大值是 320 个线程。<br /><br /> 最大值取决于按以前定义的任何自定义关联掩码可用的处理器数。 例如，如果您已将线程池关联设置为使用 32 个处理器中的 8 个，并且现在将 MaxThreads 设置为 -10，则线程池的上限将为 10 乘以 8（即 80 个线程）。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。|  
|`Process` \ `MinThreads`|ssNoversion|一种 32 位有符号整数，用于指定为线程池预分配的最小线程数。|0|0 指示由服务器确定默认值。 默认情况下，最小值为 1。<br /><br /> 如果将此值设置为负值，服务器会将此值乘以逻辑处理器数。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。|  
|`Process` \ `PriorityRatio`|ssNoversion|有符号 32 位整数，可用于确保即使高优先级队列不为空，有时也能执行低优先级线程。|2|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|`Process` \ `StackSizeKB`|ssNoversion|一种 32 位有符号整数，可用于调整线程执行期间的内存分配。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|`Query`  \ `Concurrency`|double|一个双精度浮点值，确定用于设置可同时排队的线程数目标的算法。|2.0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。<br /><br /> 并发用于初始化线程池，这些线程池使用 Windows 中的 IO 完成端口来实施。 有关详细信息，请参阅 [I/O 完成端口](http://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|`Query` \ `GroupAffinity`|string|一个十六进制值的数组，这些值与系统上的处理器组相对应，用于设置处理线程与每个处理器组中的逻辑处理器的关联。|none|可以使用此属性创建自定义关联。 该属性默认为空。<br /><br /> 有关详细信息，请参阅 [设置 GroupAffinity 以便将线程关联到处理器组中的处理器](#bkmk_groupaffinity) 。|  
|`Query`  \ `MaxThreads`|ssNoversion|有符号 32 位整数，用于指定线程池中要包含的最大线程数。|0|0 指示由服务器确定默认值。 默认情况下，服务器将此值设置为绝对值 10 或逻辑处理器数的 2 倍，以较大者为准。 例如，在 4 核超线程系统上，最大线程数 16。<br /><br /> 如果将此值设置为负值，则服务器将该值乘以逻辑处理器数。 例如，当在具有 32 个逻辑处理器的服务器上设置为 -10 时，最大值是 320 个线程。<br /><br /> 最大值取决于按以前定义的任何自定义关联掩码可用的处理器数。 例如，如果您已将线程池关联设置为使用 32 个处理器中的 8 个，并且现在将 MaxThreads 设置为 -10，则线程池的上限将为 10 乘以 8（即 80 个线程）。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。|  
|`Query` \ `MinThreads`|ssNoversion|一种 32 位有符号整数，用于指定为线程池预分配的最小线程数。|0|0 指示由服务器确定默认值。 默认情况下，最小值为 1。<br /><br /> 如果将此值设置为负值，服务器会将此值乘以逻辑处理器数。<br /><br /> 服务启动时，此线程池属性所使用的实际值即会写入 msmdsrv log 文件。<br /><br /> 可在 [Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)中找到有关优化线程池设置的详细信息。|  
|`Query` \ `PriorityRatio`|ssNoversion|有符号 32 位整数，可用于确保即使高优先级队列不为空，有时也能执行低优先级线程。|2|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
|`Query`  \ `StackSizeKB`|ssNoversion|一种 32 位有符号整数，可用于调整线程执行期间的内存分配。|0|这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。|  
  
##  <a name="bkmk_groupaffinity"></a> 设置 GroupAffinity 以便将线程关联到处理器组中的处理器  
 提供 `GroupAffinity` 仅用于高级优化用途。 可以使用`GroupAffinity`属性之间设置关联[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]线程池和特定处理器; 但是，对于大多数安装，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]时它可以使用所有可用逻辑处理器的性能最佳。 相应地，默认情况下不指定组关联。  
  
 如果性能测试表明需要进行 CPU 优化，则可以考虑高级方法，例如，使用 Windows Server Resource Manager 在逻辑处理器和服务器进程之间设置关联。 与定义个别线程池的自定义关联相比，这种方法可以简化实施和管理。  
  
 如果该方法还不够，则可以通过定义线程池的自定义关联来实现更高的精度。 由于线程池分散到的处理器范围太广，因此，在正遭遇性能降级的大型多核系统（NUMA 或非 NUMA）上更建议使用自定义关联设置。 尽管您可以在具有少于 64 个逻辑处理器的系统上设置 `GroupAffinity`，但获得的好处可以忽略不计，甚至可能会降低性能。  
  
> [!NOTE]  
>  `GroupAffinity` 受版本的约束，版本将会限制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的内核数。 在启动时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用版本信息并`GroupAffinity`要管理的 5 个线程池中的每个计算关联掩码属性[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 Standard 版本可使用最多 16 个内核。 如果在内核数超过 16 的大型多核系统上安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 标准版本， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将仅使用其中 16 个内核。 如果您升级之前版本的 Enterprise 实例，则最多可以使用 20 个内核。 有关版本和许可的详细信息，请参阅 [SQL Server 2012 许可概述](http://go.microsoft.com/fwlink/?LinkId=246061)。  
  
### <a name="syntax"></a>语法  
 该值是每个处理器组对应的十六进制值，其中十六进制表示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在为给定线程池分配线程时首先尝试使用的逻辑处理器。  
  
 **逻辑处理器的位掩码**  
  
 一个处理器组中最多可包含 64 个逻辑处理器。 对于组中由某个线程池使用（或未使用）的逻辑处理器，其位掩码为 1（或 0）。 后计算的位掩码，即可计算十六进制值的值作为`GroupAffinity`。  
  
 **多个处理器组**  
  
 处理器组在系统启动时确定。 `GroupAffinity` 接受逗号分隔列表中每个处理器组的十六进制的值。 给定多个处理器组（高端系统上最多 10 个）时，您可以通过指定 0x0 绕过个别组。 例如，在具有四个处理器组（0、1、2、3）的系统上，您可以为第一个和第三个值输入 0x0，从而排除组 0 和组 2。  
  
 `<GroupAffinity>0x0, 0xFF, 0x0, 0xFF</GroupAffinity>`  
  
### <a name="steps-for-computing-the-processor-affinity-mask"></a>计算处理器关联掩码的步骤  
 可以设置`GroupAffinity`在 msmdsrv.ini 或 SQL Server Management Studio 中的服务器属性页。  
  
1.  **确定处理器和处理器组的数目**  
  
     可以 [从 winsysinternals 下载 Coreinfo 实用工具](http://technet.microsoft.com/sysinternals/cc835722.aspx)。  
  
     运行 **coreinfo** ，从“逻辑处理器到组映射”部分获取此信息。 为每个逻辑处理器生成单独一行。  
  
2.  按从右到左顺序排列处理器： `7654 3210`  
  
     本例仅显示 8 个处理器（0 到 7），但一个处理器组最多可有 64 个逻辑处理器，而企业级 Windows 服务器中最多可有 10 个处理器组。  
  
3.  **计算想要使用的处理器组的位掩码**  
  
     `7654 3210`  
  
     使用 0 或 1 替换数字，具体取决于要排除还是包括逻辑处理器。 在具有 8 个处理器的系统上，如果要将处理器 7、6、5、4 和 1 用于 Analysis Services，则计算结果可能如下所示：  
  
     `1111 0010`  
  
4.  **将二进制数字转换为十六进制值**  
  
     使用计算器或转换工具，将二进制数转换为其对应的十六进制数。 在我们的示例中， `1111 0010` 转换为 `0xF2`。  
  
5.  **在 GroupAffinity 属性中输入该十六进制值**  
  
     在 msmdsrv.ini 或 Management Studio 中的服务器属性页中，设置`GroupAffinity`为步骤 4 中计算值。  
  
> [!IMPORTANT]  
>  设置`GroupAffinity`是一项涉及多个步骤的手动任务。 计算时`GroupAffinity`，请仔细检查您的计算。 尽管 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在整个掩码无效时返回错误，但有效和无效设置的组合会使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 忽略该属性。 例如，如果位掩码包含额外值，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 忽略该设置，并使用系统上的所有处理器。 进行此操作时没有错误或警告可提醒您，但您可检查 msmdsrv.log 文件以了解实际如何设置这些关联。  
  
##  <a name="bkmk_pernumanode"></a> 设置 PerNumaNode 以使 IO 线程与 NUMA 节点中的处理器关联  
 对于多维 Analysis Services 实例，可以设置`PerNumaNode`上`IOProcess`线程池，以进一步优化线程安排和执行。 而`GroupAffinity`标识哪组逻辑处理器用于给定的线程池，`PerNumaNode`更进一步通过指定是否创建多个线程池，进一步关联到允许的逻辑处理器的一些子集。  
  
> [!NOTE]  
>  在 Windows Server 2012 上，使用任务管理器查看计算机上的 NUMA 节点数。 在任务管理器中的“性能”选项卡上，选择 **“CPU”** ，然后右键单击图形区以查看 NUMA 节点。 或者，从 Windows Sysinternals [下载](http://technet.microsoft.com/sysinternals/cc835722.aspx) Coreinfo 实用工具，然后运行 `coreinfo –n` 以返回 NUMA 节点和每个节点中的逻辑处理器。  
  
 有效值`PerNumaNode`是-1、 0、 1、 2，如中所述[线程池属性参考](#bkmk_propref)本主题中的部分。  
  
### <a name="default-recommended"></a>默认值（建议）  
 在具有 NUMA 节点的系统上，建议使用默认设置 PerNumaNode=-1，允许 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 基于节点计数调整线程池数及其线程关联。 如果系统具有少于 4 个节点，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实现所描述的行为`PerNumaNode`= 0，而`PerNumaNode`= 1 用在具有 4 个或多个节点的系统上。  
  
### <a name="choosing-a-value"></a>选择值  
 还可以覆盖默认值以使用其他有效值。  
  
 **设置 PerNumaNode=0**  
  
 忽略 NUMA 节点。 将只有一个 IOProcess 线程池，并将使该线程池中的所有线程与所有逻辑处理器关联。 默认情况下（其中 PerNumaNode=-1），如果计算机具有的 NUMA 节点少于 4 个，则这是合适的设置。  
  
 ![Numa、 处理器和线程池通信](../media/ssas-threadpool-numaex0.PNG "Numa、 处理器和线程池通信")  
  
 **设置 PerNumaNode=1**  
  
 为每个 NUMA 节点创建 IOProcess 线程池。 具有不同的线程池可改进对本地资源（如 NUMA 节点上的本地缓存）的协调访问。  
  
 ![Numa、 处理器和线程池通信](../media/ssas-threadpool-numaex1.PNG "Numa、 处理器和线程池通信")  
  
 **设置 PerNumaNode=2**  
  
 此设置适用于运行高强度 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作负荷的非常高端的系统。 此属性会在其最高粒度级别上设置 IOProcess 线程池关联，在逻辑处理器层面创建和关联单独的线程池。  
  
 在以下示例中，在系统上具有 4 个 NUMA 节点和 32 个逻辑处理器，设置`PerNumaNode`为 2 会产生 32 个 IOProcess 线程池。 前 8 个线程池中的线程将关联到 NUMA 节点 0 中的所有逻辑处理器，但理想的处理器设置为 0、1、2 直到 7。 接下来的 8 个线程池将关联到 NUMA 节点 1 中的所有逻辑处理器，而理想的处理器设置为 8、9、10 直到 15，以此类推。  
  
 ![Numa、 处理器和线程池通信](../media/ssas-threadpool-numaex2.PNG "Numa、 处理器和线程池通信")  
  
 在此关联水平上，计划程序始终会尝试先使用首选 NUMA 节点内的理想逻辑处理器。 如果逻辑处理器不可用，计划程序将选择同一节点内的另一个处理器，或在其他线程不可用时选择同一处理器组中的处理器。 有关详细信息和示例，请参阅 [Analysis Services 2012 配置设置（Wordpress 博客）](http://go.microsoft.com/fwlink/?LinkId=330387)。  
  
###  <a name="bkmk_workdistrib"></a> IOProcess 线程间的工作分配  
 当您考虑是否设置`PerNumaNode`属性，知道如何`IOProcess`使用线程可帮助您做出更明智的决策。  
  
 请记住，`IOProcess`用于与多维引擎中的存储引擎查询关联的 IO 作业。  
  
 扫描某段后，引擎将识别该段所属的分区，并尝试将该段作业排入该分区所用线程池的队列。 一般而言，属于分区的所有段都将其任务排入同一线程池的队列。 在 NUMA 系统中，此行为尤其具有优势，因为对分区的所有扫描都将使用文件系统缓存中在本地分配给该 NUMA 节点的内存。  
  
 以下方案提出一些建议调整，在某些情况下可提高对 NUMA 系统的查询性能：  
  
-   对于分区不足的度量值组（例如，具有一个分区），请增加分区数。 只使用一个分区会使该引擎始终将任务排队进入一个线程池（线程池 0）。 添加更多分区使该引擎可以使用其他线程池。  
  
     或者，如果您不能创建其他分区，请尝试设置`PerNumaNode`= 0，以一种方法，以提高对线程池 0 可用的线程数。  
  
-   对于将段扫描均匀分布到多个分区，设置的数据库`PerNumaNode`为 1 或 2 可以提高查询性能因为增加的总体数目`IOProcess`线程池使用的系统。  
  
-   对于具有多个分区，但只有一个很大程度扫描的解决方案，请尝试设置`PerNumaNode`= 0，以确定是否可以改进性能。  
  
 尽管分区和维度扫描都使用`IOProcess`线程池，但维度扫描仅使用线程池 0。 这样可导致该线程池上的负载略有不均，但这种不平衡只是暂时性的，因为维度扫描往往速度很快且不常见。  
  
> [!NOTE]  
>  在更改服务器属性时，请记住，配置选项适用于在当前实例上运行的所有数据库。 选择可使最重要数据库或最大数量的数据库受益的设置。 您不能在数据库级别设置处理器关联，也不能在单个分区与特定处理器之间设置关联。  
  
 有关作业体系结构的详细信息，请参阅 [SQL Server 2008 Analysis Services 性能指南](http://www.microsoft.com/download/details.aspx?id=17303)中的 2.2 节。  
  
##  <a name="bkmk_related"></a> 依赖或相关属性  
 中的第 2.4 节所述[Analysis Services 操作指南](http://msdn.microsoft.com/library/hh226085.aspx)，如果您增大处理线程池，应确保`CoordinatorExecutionMode`设置，并将`CoordinatorQueryMaxThreads`设置的值，使您能够充分利用增加的线程池大小。  
  
 Analysis Services 使用一种协调器线程来收集必要的数据，以便完成处理或查询请求。 对于必须触及的每个分区，协调器首先将一个作业加入队列。 随后，其中每个作业又会使更多作业排队等候，具体取决于必须在分区中扫描的段总数。  
  
 `CoordinatorExecutionMode` 的默认值为 -4，表示每个内核可并行运行 4 个作业，这样可约束存储引擎中的子多维数据集请求可并行执行的协调器作业总数。  
  
 默认值为`CoordinatorQueryMaxThreads`为 16，这就限制了可以为每个分区并行执行的段作业数。  
  
##  <a name="bkmk_currentsettings"></a> 确定当前线程池设置  
 服务每次启动时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 都会将当前线程池设置输出到 msmdsrv.log 文件中，包括最小和最大线程数、处理器关联掩码和并发度。  
  
 以下示例摘自该日志文件，显示启用超线程的 4 核系统上的查询线程池默认设置（MinThread=0、MaxThread=0、Concurrency=2）。 关联掩码为 0xFF，表示有 8 个逻辑处理器。 请注意，掩码以前导零为前缀。 可以忽略前导零。  
  
 `"10/28/2013 9:20:52 AM) Message: The Query thread pool now has 1 minimum threads, 16 maximum threads, and a concurrency of 16.  Its thread pool affinity mask is 0x00000000000000ff. (Source: \\?\C:\Program Files\Microsoft SQL Server\MSAS11.MSSQLSERVER\OLAP\Log\msmdsrv.log, Type: 1, Category: 289, Event ID: 0x4121000A)"`  
  
 请记住，用于设置 **MinThread** 和 **MaxThread** 的算法包括系统配置，具体说就是处理器数目。 以下博客文章深入介绍了这些值的计算方式： [Analysis Services 2012 配置设置（Wordpress 博客）](http://go.microsoft.com/fwlink/?LinkId=330387)。 请注意，这些设置和行为会在后续版本中做出调整。  
  
 以下列表显示在处理器的不同组合下其他关联掩码设置的示例：  
  
-   8 核系统上处理器 3-2-1-0 的关联生成位掩码 00001111 和十六进制值 0xF  
  
-   8 核系统上处理器 7-6-5-4 的关联生成位掩码 11110000 和十六进制值 0xF0  
  
-   8 核系统上处理器 5-4-3-2 的关联生成位掩码 00111100 和十六进制值 0x3C  
  
-   8 核系统上处理器 7-6-1-0 的关联生成位掩码 11000011 和十六进制值 0xC3  
  
 回想一下，在具有多个处理器组的系统上，系统会以逗号分隔列表的形式为每个组生成单独的关联掩码。  
  
##  <a name="bkmk_msmdrsrvini"></a> 关于 MSMDSRV.INI  
 msmdsrv.ini 文件包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的配置设置，会影响运行在该实例上的所有数据库。 您不能使用服务器配置属性仅优化一个数据库的性能，而将所有其他数据库排除在外。 但是，您可以安装多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例并将每个实例配置为使用将使具有类似特征或工作负荷的数据库受益的属性。  
  
 所有服务器配置属性都包括在 msmdsrv.ini 文件中。 很可能要修改的部分属性还出现诸如 SSMS 的管理工具中。  
  
 表格和多维 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的 msmdsrv.ini 内容是相同的。 但是，有些设置仅适用于一种模式。 基于服务器模式的行为差异记录在属性参考文档中。  
  
> [!NOTE]  
>  有关如何设置属性的说明，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [关于进程和线程](http://msdn.microsoft.com/library/windows/desktop/ms681917\(v=vs.85\).aspx)   
 [多个处理器](http://msdn.microsoft.com/library/windows/desktop/ms684251\(v=vs.85\).aspx)   
 [处理器组](http://msdn.microsoft.com/library/windows/desktop/dd405503\(v=vs.85\).aspx)   
 [SQL Server 2012 中的 analysis Services 线程池更改](http://blogs.msdn.com/b/psssql/archive/2012/01/31/analysis-services-thread-pool-changes-in-sql-server-2012.aspx)   
 [Analysis Services 2012 配置设置 （Wordpress 博客）](http://go.microsoft.com/fwlink/?LinkId=330387)   
 [支持具有 64 个以上处理器的系统](http://msdn.microsoft.com/library/windows/hardware/gg463349.aspx)   
 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)  
  
  
