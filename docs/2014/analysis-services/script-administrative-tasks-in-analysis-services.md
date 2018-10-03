---
title: 编写 Analysis Services 中的管理任务脚本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic Analysis Services administration
- administering Analysis Services
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11385dd002acd7b0181422aaa571fe8fe46f188c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186067"
---
# <a name="script-administrative-tasks-in-analysis-services"></a>在 Analysis Services 中编写管理任务脚本
  您可以通过编写或生成可手动执行或通过 SQL Server 代理来计划的脚本自动执行 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 管理任务。 下表总结了可供您使用的脚本编写选项，并提供指向更多信息的链接。  
  
 下面所列的所有方法都支持脚本保存到文件中，然后作为独立操作执行。 由于在表格模型和 PowerPivot 工作簿中使用的数据分析表达式 (DAX) 语言不符合条件，所以未包含在下面的列表中。  
  
|方法|文件格式|Description|链接|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|Analysis Services 通过一个新的访问接口（从命令行添加对象导航）以及新增的用于管理任务（如备份、还原、处理和角色管理）的 cmdlet 来支持 SQL Server PowerShell 脚本环境。<br /><br /> 此外，SQL Server PowerPivot (SQLPS) 访问接口还包括一个通用的 cmdlet `Invoke-ASCmd`，它支持您从 PowerShell 会话内部运行 XMLA、MDX 或 DMX 脚本文件。<br /><br /> 多维模型和表格模型均支持 Analysis Services PowerShell 脚本，但从 SharePoint 访问的 PowerPivot 工作簿却不支持该脚本。|[Analysis Services PowerShell](analysis-services-powershell.md)<br /><br /> [Windows PowerShell 生存指南](http://go.microsoft.com/fwlink/?LinkId=233747)|  
|ASSL 或 XMLA 脚本|.xmla|Analysis Services 脚本语言 (ASSL) 是对 XMLA 的扩展，该语言提供针对在表格或多维模式中运行的 Analysis Services 实例上的对象和操作的数据访问。 ASSL 包括数据定义和命令语言支持，支持以 XML 格式完整表示 Analysis Services 对象和操作。 使用 ASSL 提供的对象和命令的脚本另存为 .xmla 文件。 在 Analysis Services 的上下文内，通常将 ASSL 视为 XMLA 脚本。 当您具有以下要求时，请选择这种方法：<br /><br /> 您的脚本直接在服务器上创建对象，或执行数据定义和操作任务（例如，重新创建和处理数据库）。<br /><br /> 您需要在多种工具和技术中最大程度地重复使用脚本。 可以在 SQL Server 代理中将 XMLA 脚本添加到 Analysis Services 命令任务，在 SSIS 包或 PowerShell 脚本中引用 XMLA 脚本。<br /><br /> 必须以无人参与的模式运行该脚本。 可以使用 SQL Server 代理调度包含 XMLA 脚本的作业或包含 XMLA 的 SSIS 包。<br /><br /> 您的应用程序要求使用 XMLA。 XMLA 是一个不需要托管代码环境的接口。 您可以在不使用 .NET Framework 的应用程序中执行 XMLA 脚本。|[在 Management Studio 中创建 Analysis Services 脚本](instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [使用 SQL Server 代理来计划 SSAS 管理任务](instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [开发使用 Analysis Services 脚本语言&#40;ASSL&#41;](multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd cmdlet](/sql/analysis-services/powershell/invoke-ascmd-cmdlet)|  
|||若要创建 XMLA 脚本，您可以在 Management Studio 中使用脚本生成器。 在对象级别，右键单击某个对象可生成创建、更改或删除对象的脚本。 在命令级别，例如在执行处理、备份或还原、聚合设计或执行另一个命令时，您可以使用相应对话框中的脚本功能，通过选择将脚本放入新的窗口、文件或剪贴板等选项来生成脚本。 您也可以在文本或代码编辑器中手动编写 XMLA 脚本，或使用模板资源管理器中的模板编写 XMLA 脚本。 若要运行该脚本，请使用以下方法之一：<br /><br /> 使用 Management Studio 直接在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上创建或修改对象。<br /><br /> 使用 SQL Server 代理调度包括 Analysis Services 命令任务的作业。<br /><br /> 使用 Invoke-ASCmd cmdlet 在 PowerShell 会话中运行该脚本。||  
|MDX 脚本|.mdx|多维表达式 (MDX) 语言是一种用于分析数据源的业界标准查询语言，它同样也是 XMLA 规范的一部分。<br /><br /> 您可以创建用来查询数据或系统信息的独立 MDX 脚本文件。 例如，可以通过 MDX Select 语句来访问公开与本地服务器操作和服务器运行状况有关的信息的动态管理视图 (DMV)。<br /><br /> MDX 脚本可在多维和表格模式的服务器上运行。 您可以使用 `Invoke-ASCmd` 从 SQL Server Management Studio 或 PowerShell 会话以交互方式运行该脚本。|[MDX 脚本编写基础知识&#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [使用动态管理视图&#40;Dmv&#41;若要监视 Analysis Services](instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX 脚本|.dmx|数据挖掘扩展插件 (DMX) 是用于数据挖掘模型的数据定义、数据操作和数据查询语言。 您可以借助模板来入门。|[在 SQL Server Management Studio 中创建 DMX 查询](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 模板](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 包|.dtsx|[!INCLUDE[ssIS](../includes/ssis-md.md)] 提供任务和数据流可用于创建、 修改、 删除和处理 Analysis Services 对象，其中包括数据挖掘模型。 可以使用 SQL Server 代理调度要运行的包。|[Analysis Services 执行 DDL 任务](../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Analysis Services 处理任务](../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [数据挖掘查询任务](../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [数据挖掘模型定型目标](../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [维度处理目标](../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [分区处理目标](../integration-services/data-flow/partition-processing-destination.md)|  
|分析管理对象||分析管理对象 (AMO) 是一种托管接口，编程人员可用它来开发自动执行管理操作的自定义应用程序。 使用 AMO，您可以开发运行您提供的 XMLA、MDX 或 DMX 脚本的自定义应用程序。|[使用 AMO 对管理任务进行编程](multidimensional-models/analysis-management-objects/programming-administrative-tasks-with-amo.md)|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言&#40;ASSL&#41;引用](scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [使用分析管理对象开发&#40;AMO&#41;](multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)   
 [多维模型对象处理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
