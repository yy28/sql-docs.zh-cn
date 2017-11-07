---
title: "用于处理 (Analysis Services) 工具和方法 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5eecf424cf155c53a2f636590ba002028f24db84
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>用于处理的工具和方法 (Analysis Services)
  处理是指这样一项操作：Analysis Services 查询关系数据源并使用该数据填充 Analysis Services 对象。  
  
 作为 Analysis Services 系统管理员，您可以使用以下方法执行并监视 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的处理：  
  
-   运行影响分析，了解对象依赖关系和操作的作用域  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   运行影响分析，检查由于当前操作而不会处理的相关对象的列表。  
  
-   在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] XMLA 查询窗口中生成并运行脚本，以便处理单个或多个对象  
  
-   使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell cmdlet  
  
-   使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包中的控制流和任务  
  
-   使用 SQL Server Profiler 监视处理  
  
-   使用 AMO 对自定义解决方案编程。 有关详细信息，请参阅 [Programming AMO OLAP Basic Objects](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)。  
  
 处理是由一组处理选项控制的高度可配置操作，这些选项决定在对象级别执行完全处理还是增量处理。 有关处理选项和对象的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md) 和[处理 Analysis Services 对象](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)。  
  
> [!NOTE]  
>  本主题介绍用于处理多维模型的工具和方法。 有关处理表格模型的详细信息，请参阅[处理数据库、表或分区 (Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md) 和[处理数据（SSAS 表格）](../../analysis-services/tabular-models/process-data-ssas-tabular.md)。  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中处理对象  
  
1.  启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 并连接到 Analysis Services。  
  
2.  右键单击要处理的 Analysis Services 对象，然后单击“处理”。 可以在以下任何级别处理数据：  
  
    -   “数据库”  
  
    -   多维数据集  
  
    -   度量值组或度量值组中的各个分区  
  
    -   维度  
  
    -   挖掘模型  
  
    -   挖掘结构  
  
     Analysis Services 对象具有层次结构。 如果选择数据库，则可能处理该数据库中包含的所有对象。 是否实际进行处理将根据您选择的处理选项和对象的状态而有所不同。 具体而言，如果某个对象尚未处理，则处理其父级将导致处理该对象。 有关对象依赖关系的详细信息，请参阅 [Processing Analysis Services Objects](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)。  
  
3.  在 **“处理”** 对话框中的 **“处理选项”**中，使用提供的默认值或从列表中选择一个不同的选项。 有关每个选项的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
4.  如果“处理”对话框中列出的对象已处理，则单击 **“影响分析”** 可以标识受影响的依赖对象，并且根据需要处理这些依赖对象。  
  
5.  还可以单击 **“更改设置”** 来修改处理顺序、与特定类型的错误相关的处理行为或其他设置。  
  
6.  单击 **“确定”**。  
  
     “处理进度”对话框为每个命令提供当前状态。 如果状态消息被截断，则可以单击 **“查看详细信息”** 来读取完整消息。  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中处理对象  
  
1.  启动 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 并打开已部署的项目。  
  
2.  在解决方案资源管理器中，在已部署项目下，展开 **“维度”** 文件夹。  
  
3.  右键单击某个维度，然后单击“处理”。 您可以右键单击多个维度，以便一次处理多个对象。 有关详细信息，请参阅[批处理 (Analysis Services)](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)。  
  
4.  在 **“处理维度”** 对话框的 **“对象列表”** 下的 **“处理选项”**列中，验证此列的选项是否为 **“处理全部”**。 如果不是，则在“处理选项”中单击选项，并从下拉列表中选择“处理全部”。  
  
5.  单击 **“运行”**。  
  
6.  处理结束时，单击 **“关闭”**。  
  
##  <a name="bkmk_impactanalysis"></a> 运行影响分析，以确定对象依赖关系和操作的作用域  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中处理 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]对象之前，可以通过单击 **“处理对象”** 对话框之一中的 **“影响分析”** 来分析对相关对象的影响。  
  
2.  右键单击某个维度、多维数据集、度量值组或分区，打开“处理对象”对话框。  
  
3.  单击 **“影响分析”**。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将为与选定要处理的对象相关的对象扫描模型并报告重新处理要求。  
  
### <a name="processing-objects-using-xmla"></a>使用 XMLA 处理对象  
  
1.  启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 并连接到 Analysis Services。  
  
2.  右键单击待处理的对象，然后单击“处理”。  
  
3.  在 **“处理”** 对话框中，选择要使用的处理选项。 修改任何其他设置。 运行“影响分析”以标识您可能需要进行的任何更改。  
  
4.  单击 **“处理对象”** 屏幕上的 **“脚本”** 。  
  
     这将生成一个 XMLA 脚本并打开一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA 查询窗口。  
  
5.  关闭“添加或删除程序” 对话框。 该脚本包含在该对话框中指定的处理命令和选项。  
  
6.  或者，如果您要在同一批中处理其他对象，则可以继续向该脚本添加对象。 若要继续操作，请重复之前的步骤，追加生成的脚本，这样您可以在一个脚本中包含所有要处理的操作。 若要查看示例，请参阅 [Schedule SSAS Administrative Tasks with SQL Server Agent](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)。  
  
7.  在菜单栏中，单击 **“查询”**，然后单击 **“执行”**。  
  
### <a name="processing-objects-using-powershell"></a>使用 PowerShell 处理对象  
  
1.  从本版本的 SQL Server 开始，您可以使用 Analysis Services PowerShell cmdlet 来处理对象。 可以通过交互方式或在脚本中运行以下 cmdlet：  
  
    -   [Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)可用于执行包含处理命令的 XMLA、MDX 或 DMX 脚本。  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>使用 SQL Server Profiler 监视对象处理  
  
1.  在 SQL Server Profiler 中，连接到 Analysis Services 实例。  
  
2.  在“事件选择”中，单击 **“显示所有事件”** ，将所有事件添加到列表中。  
  
3.  选择以下事件：  
  
    -   **“命令开始”** 和 **“命令结束”** ，显示处理启动和停止的时间  
  
    -   **“错误”** ，捕获任何错误  
  
    -   **“进度报告开始”**、 **“进度报告当前状态”**和 **“进度报告结束”** ，报告处理状态并显示用于检索数据的 SQL 查询  
  
    -   **“开始执行 MDX 脚本”** 和 **“结束执行 MDX 脚本”** ，显示多维数据集的计算  
  
    -   或者，如果您在诊断与处理相关的性能问题，则可以添加锁事件  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>使用 Integration Services 处理 Analysis Services 对象  
  
1.  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，创建一个使用 Analysis Services 处理任务的包，以便在对源关系数据库进行定期更新时使用新数据自动填充对象。  
  
2.  在“SSIS 工具箱”中，双击“Analysis Services 处理”将其添加到包中。  
  
3.  编辑该任务，指定与数据库的连接、处理哪些对象以及处理选项。 有关如何执行此任务的详细信息，请参阅 [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)。  
  
## <a name="see-also"></a>另请参阅  
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  

