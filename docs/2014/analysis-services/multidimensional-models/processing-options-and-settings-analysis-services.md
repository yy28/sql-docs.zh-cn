---
title: 处理选项和设置（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process data option [Analysis Services]
- processing objects [Analysis Services]
- unprocess option [Analysis Services]
- process full option [Analysis Services]
- process index option [Analysis Services]
- process structure option [Analysis Services]
- process incremental option [Analysis Services]
- process update option [Analysis Services]
- process clear structure option [Analysis Services]
- process default option [Analysis Services]
ms.assetid: 2e858c74-ad3e-45f1-8745-efe2c0c3a7fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe4851712f56acd5d23e8762584968b1cecad03c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073219"
---
# <a name="processing-options-and-settings-analysis-services"></a>处理选项和设置 (Analysis Services)
  在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]处理对象时，您可以选择处理选项以控制每个对象发生的处理的类型。 处理类型因对象而异，并基于自上次处理对象后对象所发生的更改。 如果允许 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动选择处理方法，则将使用以最少时间将对象返回已完全处理状态的方法。  
  
 通过处理设置可以控制要处理的对象以及用来处理这些对象的方法。 某些处理设置主要用于批处理作业。 有关批处理的详细信息，请参阅[批处理 (Analysis Services)](batch-processing-analysis-services.md)。  
  
> [!NOTE]  
>  本主题适用于多维和数据挖掘解决方案。 有关表格解决方案的信息，请参阅[处理数据库、表或分区](../tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="processing-options"></a>处理选项  
 下表介绍了可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中使用的处理方法，并标识了支持每种方法的对象。  
  
|“模式”|适用于|说明|  
|----------|----------------|-----------------|  
|**处理默认值**|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。|检测数据库对象的处理状态，进行必要的处理，将未处理对象或部分处理的对象转变成为已完全处理的对象。 如果更改数据绑定，“处理默认值”将对受影响的对象执行“处理全部”。|  
|**处理全部**|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。|处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象及其包含的所有对象。 对已被处理的对象执行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 如果对对象进行了结构更改（例如，添加、删除或重命名属性层次结构），则需要此类处理。|  
|**处理清除**|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。|删除指定对象和任何低级构成对象中的数据。 该数据被删除后将不会被重新加载。|  
|**处理数据**|维度、多维数据集、度量值组和分区。|只处理数据，而不生成聚合或索引。 如果分区中有数据，则先删除数据，然后使用源数据重新填充分区。|  
|**处理添加**|维度、度量值组和分区<br /><br /> 注意：“处理添加”  对于 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的维度处理不可用，但是你可以编写 XMLA 脚本执行此操作。|对于维度，添加新成员并更新维度属性标题和说明。<br /><br /> 对于度量值组和分区，添加新的可用事实数据并只处理相关分区。|  
|**处理更新**|维度|强制重新读取数据并更新维度属性。 将删除对相关分区的灵活聚合和索引。|  
|**处理索引**|多维数据集、维度、度量值组和分区|为所有已处理的分区创建或重新生成索引和聚合。 对于未处理的对象，此选项会生成错误。<br /><br /> 如果关闭“迟缓处理”，则需要使用此选项进行处理。|  
|**处理结构**|多维数据集和挖掘结构|如果未处理多维数据集，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在必要时处理该多维数据集的所有维度。 然后， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将只创建多维数据集定义。 如果将此选项应用于挖掘结构，则它将使用源数据填充挖掘结构。 此选项与“处理完全”选项之间的区别在于此选项不在挖掘模型自身中向下迭代处理。|  
|**处理清除结构**|挖掘结构|从挖掘结构中删除所有定型数据。|  
  
## <a name="processing-settings"></a>处理设置  
 下表说明在创建处理操作时可以使用的处理设置。  
  
|处理选项|说明|  
|-----------------------|-----------------|  
|**并行**|用于批处理。 此设置会使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将处理任务分开在单个事务内并行执行。 如果出现故障，则结果是回滚所有更改。 您可以显式设置并行任务的最大数目，或者让服务器确定最佳分布。 “并行”选项对于提高处理速度十分有用。|  
|**按顺序（事务模式）**|控制处理作业的执行行为。 使用 **“一项事务”** 进行处理时，将在处理作业成功后提交所有更改。 也就是说，受特定处理作业影响的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象将保持对查询可用，直到提交进程为止。 这样，对象会暂时不可用。 使用 **“单独的事务”** 将使处理作业中受某进程影响的所有对象一旦在该进程成功后就无法用于查询。 两个可用选项是：<br /><br /> **一项事务**。 处理作业作为事务运行。 如果处理作业内的所有进程都成功，则提交处理作业所做的所有更改。 如果有一个进程失败，则回滚处理作业所做的所有更改。 **“一项事务”** 是默认值。<br /><br /> **单独的事务**。 处理作业中的每个进程都作为独立的作业运行。 如果某个进程失败，则仅回滚该进程，处理作业继续执行。 每个作业将在作业结束时提交所有进程更改。|  
|**写回表选项**|控制在处理过程中如何处理写回表。 此选项应用于多维数据集中的写回分区，有下列选项可供使用：<br /><br /> **使用现有**的。 使用现有的写回表。 这是默认值。<br /><br /> **Create**。 创建一个新的写回表，如果已经存在一个写回表，则会导致进程失败。<br /><br /> **始终创建**。 即使已经存在一个写回表，也要创建一个新的写回表。 现有表将被删除和替换。|  
|**处理受影响的对象**|控制处理作业的对象范围。 受影响的对象由对象依赖关系定义。 例如，分区依赖于确定聚合的维度，但是维度不依赖于分区。 您可以使用下列选项：<br /><br /> **False**。 作业将处理作业中显式命名的对象以及所有依赖对象。 例如，如果处理作业仅包含维度，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅处理作业中显式标识的那些对象。 如果处理作业包含分区，分区处理将自动调用受影响维度的处理。 **“False”** 是默认设置。<br /><br /> **True**。 作业将处理作业中显式命名的对象、所有依赖对象以及受正在处理的对象影响的所有对象（不更改受影响对象的状态）。 例如，如果处理作业仅包含维度， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还将处理受当前已处理分区的维度处理影响的所有分区。 如果受影响分区当前处于未处理状态，则不会对其进行处理。 不过，由于分区依赖于维度，因此如果处理作业仅包含分区，分区处理将自动调用受影响维度的处理，即使维度当前处于未处理状态也是如此。|  
|**维度键错误**|确定在处理过程中发生错误时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行的操作。 选择“使用默认错误配置”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用针对要处理的每个对象设置的错误配置。 如果将对象设置为使用默认的配置设置，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用为每个选项列出的默认设置。 选择 "**使用自定义错误配置**" 时，可以选择以下操作的值来控制错误处理行为：<br /><br /> **键错误操作**。 如果记录中并不存在某个键值，则选择执行下列一项操作：<br /><br /> **转换为未知**。 键被解释为未知成员。 这是默认设置。<br /><br /> **放弃记录**。 将放弃记录。|  
||**处理错误限制**。 通过选择下列一个选项控制处理的错误数：<br /><br /> **忽略错误计数**。 这将使处理继续进行，而不管错误数是多少。 <br />**出错时停止**。 使用此选项，您可以控制其他两项设置。 **“错误数”** 可以限制在出现特定错误数之后处理。 **“出错时要执行的操作”** 允许您确定达到 **“错误数”** 时的操作。 您可以选择 **“停止处理”**，这将使处理作业失败并回滚任何更改；也可以选择 **“停止日志记录”**，这将使处理继续进行，而不记录错误。 **“出错时停止”** 是默认设置，其中 **“错误数”** 设置为 **0** ， **“出错时要执行的操作”** 设置为 **“停止处理”**。|  
||特定错误条件。 您可以设置下列选项来控制特定的错误处理行为：<br /><br /> **找不到键**。 当键值存在于分区中，但不存在于相应的维度中时发生。 默认设置是 **“报告并继续”**。 其他设置是 **“忽略错误”** 和 **“报告并停止”**。<br /><br /> **重复键**。 当维度中存在多个键值时发生。 默认设置是 **“忽略错误”**。 其他设置是 **“报告并继续”** 和 **“报告并停止”**。<br /><br /> **空键转换为未知键**。 当键值为空值且 **“键错误操作”** 设置为 **“转换为未知”** 时发生。 默认设置是 **“忽略错误”**。 其他设置是 **“报告并继续”** 和 **“报告并停止”**。<br /><br /> **不允许空键**。 当 **“键错误操作”** 设置为 **“放弃记录”** 时发生。 默认设置是 **“报告并继续”**。 其他设置是 **“忽略错误”** 和 **“报告并停止”**。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型对象处理](processing-a-multidimensional-model-analysis-services.md)  
  
  
