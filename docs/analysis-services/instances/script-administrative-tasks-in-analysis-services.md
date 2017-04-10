---
title: "在 Analysis Services 中编写管理任务脚本 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "自动执行 Analysis Services 管理"
  - "管理 Analysis Services"
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
caps.latest.revision: 46
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 46
---
# 在 Analysis Services 中编写管理任务脚本
  您可以通过编写或生成可手动执行或通过 SQL Server 代理来计划的脚本自动执行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理任务。 下表总结了可供您使用的脚本编写选项，并提供指向更多信息的链接。  
  
 下面所列的所有方法都支持脚本保存到文件中，然后作为独立操作执行。 由于在表格模型和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中使用的数据分析表达式 (DAX) 语言不符合条件，所以未包含在下面的列表中。  
  
|方法|文件格式|Description|链接|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|Analysis Services 通过 SQLAS 提供程序（从命令行添加对象导航）以及用于管理任务（如备份、还原、处理和角色管理）的 cmdlet 来支持 SQL Server PowerShell 脚本环境。<br /><br /> 此外，提供程序还包括一个通用的 cmdlet **Invoke-ASCmd**，它支持你从 PowerShell 会话内部运行 TMSL、ASSL-XMLA、MDX 或 DMX 脚本文件。<br /><br /> 多维模型和表格模型均支持 Analysis Services PowerShell 脚本，但从 SharePoint 访问的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿却不支持该脚本。|[PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)|  
|TMSL|.json|表格模型脚本语言 (TMSL) 是 XMLA 的一个扩展插件，可在 SQL Server 2016 服务器上为表格模型提供命令接口和对象定义。<br /><br /> 当你具有以下任意要求时，请选择这种方法：<br /><br /> -   模型或数据库为表格 1200 兼容级别。<br />-   你的脚本直接在服务器上创建对象，或执行数据定义和操作任务（例如，重新创建和处理数据库）。<br />-   优先跨多个工具和技术进行重复使用。 可以在 SQL Server 代理中将 TMSL 脚本添加到 Analysis Services 命令任务，在 SSIS 包或 PowerShell 脚本中引用 TMSL 脚本。<br />-   必须以无人参与的模式运行该脚本。 可以使用 SQL Server 代理调度包含 TMSL 脚本的作业或包含 XMLA 的 SSIS 包。<br />-   XMLA 是一项应用程序要求。 XMLA 是一个不需要托管代码环境的接口。 您可以在不使用 .NET Framework 的应用程序中执行 XMLA 脚本。|[表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)<br /><br /> [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)<br /><br /> [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)|  
|ASSL 或 XMLA 脚本|.xmla|Analysis Services 脚本语言 (ASSL) 是对 XMLA 的扩展，该语言提供针对在表格或多维模式中运行的 Analysis Services 实例上的对象和操作的数据访问。 ASSL 包括数据定义和命令语言支持，支持以 XML 格式完整表示 Analysis Services 对象和操作。 使用 ASSL 提供的对象和命令的脚本另存为 .xmla 文件。 在 Analysis Services 的上下文内，通常将 ASSL 视为 XMLA 脚本。<br /><br /> 当你具有以下任意要求时，请选择这种方法：<br /><br /> -   模型或数据库为多维或者是低兼容级别的表格（1050、1100、1103）。<br />-   你的脚本直接在服务器上创建对象，或执行数据定义和操作任务（例如，重新创建和处理数据库）。<br />-   优先跨多个工具和技术进行重复使用。 可以在 SQL Server 代理中将 XMLA 脚本添加到 Analysis Services 命令任务，在 SSIS 包或 PowerShell 脚本中引用 XMLA 脚本。<br />-   必须以无人参与的模式运行该脚本。 可以使用 SQL Server 代理调度包含 XMLA 脚本的作业或包含 XMLA 的 SSIS 包。<br />-   XMLA 是一项应用程序要求。 XMLA 是一个不需要托管代码环境的接口。 您可以在不使用 .NET Framework 的应用程序中执行 XMLA 脚本。|[在 Management Studio 中创建 Analysis Services 脚本](../../analysis-services/instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [使用 SQL Server 代理来计划 SSAS 管理任务](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [使用 Analysis Services 脚本语言 (ASSL) 开发](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|  
|||若要创建 ASSL/XMLA 脚本，你可以在 Management Studio 中使用脚本生成器。 在对象级别，右键单击某个对象可生成创建、更改或删除对象的脚本。 在命令级别，例如在执行处理、备份或还原、聚合设计或执行另一个命令时，您可以使用相应对话框中的脚本功能，通过选择将脚本放入新的窗口、文件或剪贴板等选项来生成脚本。 您也可以在文本或代码编辑器中手动编写 XMLA 脚本，或使用模板资源管理器中的模板编写 XMLA 脚本。<br /><br /> 若要运行该脚本，请使用以下方法之一：<br /><br /> -   使用 Management Studio 直接在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上创建或修改对象。<br />-   使用 SQL Server 代理调度包括 Analysis Services 命令任务的作业。<br />-   使用 Invoke-ASCmd cmdlet 在 PowerShell 会话中运行该脚本。 请参阅 [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)。|[在 Management Studio 中创建 Analysis Services 脚本](../../analysis-services/instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [使用 SQL Server 代理来计划 SSAS 管理任务](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [使用 Analysis Services 脚本语言 (ASSL) 开发](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|  
|MDX 脚本|.mdx|多维表达式 (MDX) 语言是一种用于分析数据源的业界标准查询和表达式语言，它同样也是 XMLA 规范的一部分。<br /><br /> 您可以创建用来查询数据或系统信息的独立 MDX 脚本文件。 例如，可以通过 MDX Select 语句来访问公开与本地服务器操作和服务器运行状况有关的信息的动态管理视图 (DMV)。<br /><br /> MDX 脚本可在多维和早期表格模式的服务器上运行。 可以使用 **Invoke-ASCmd** 从 SQL Server Management Studio 或 PowerShell 会话以交互方式运行该脚本。|[MDX 脚本编写基础知识 (Analysis Services)](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [使用动态管理视图 (DMV) 监视 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX 脚本|.dmx|数据挖掘扩展插件 (DMX) 是用于数据挖掘模型的数据定义、数据操作和数据查询语言。 您可以借助模板来入门。|[在 SQL Server Management Studio 中创建一个 DMX 查询](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 包|.dtsx|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 提供的任务和数据流可用于创建、修改、删除和处理 Analysis Services 对象（包括数据挖掘模型）。 可以使用 SQL Server 代理调度要运行的包。|[Analysis Services 执行 DDL 任务](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Analysis Services 处理任务](../../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [数据挖掘查询任务](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [数据挖掘模型定型目标](../../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [维度处理目标](../../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [分区处理目标](../../integration-services/data-flow/partition-processing-destination.md)|  
|分析管理对象||分析管理对象 (AMO) 是一种托管接口，编程人员可用它来开发自动执行管理操作的自定义应用程序。 使用 AMO，你可以开发运行你提供的 TMSL、XMLA、MDX 或 DMX 脚本的自定义应用程序。|[使用 AMO 对管理任务进行编程](../../analysis-services/multidimensional-models/analysis-management-objects/programming-administrative-tasks-with-amo.md)|  
  
## 另请参阅  
 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  