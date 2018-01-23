---
title: "什么 &#39; s Analysis Services 中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 03/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: "97"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: f6645a2a5da1e63050c0d448bc1006c85d85f212
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="what39s-new-in-analysis-services"></a>什么 &#39; s Analysis Services 中的新增功能
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

SQL Server 2016 Analysis Services 包含许多提供改进的性能、 更轻松解决方案创作、 自动的数据库管理新的增强功能，与双向交叉筛选，增强的关系的并行分区处理和其他更多。 此版本的大多数增强功能的核心是表格模型数据库的全新 1200 兼容级别。     

## <a name="azure-analysis-services"></a>Azure Analysis Services
公布于 2016 SQL PASS 大会的 Analysis Services 现已作为一项 Azure 服务在云中推出。 **Azure Analysis Services**支持 1200年或更高的兼容性级别的表格模型。 可支持 DirectQuery、分区、行级安全性、双向关系和翻译。 若要了解详细信息并免费试用，请参阅 [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/)。 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>SQL Server 2016 Service Pack 1 (SP1) Analysis Services 中的新增功能

[下载 SQL Server 2016 SP1](http://www.microsoft.com/download/details.aspx?id=54276) 

SQL Server 2016 Service SP1 Analysis Services 基于 **Intel 线程构建模块** (Intel TBB)，通过非一致性内存访问 (NUMA) 感知和优化内存分配提供改进的性能和可伸缩性。 这一新功能通过在更少、功能更强大的企业服务器上支持更多的用户，有助于降低总拥有成本 (TCO)。 

SQL Server 2016 SP1 Analysis Services 特别在以下关键领域进行了改进：

-   **NUMA 感知** - 为改善 NUMA 支持，现在 Analysis Services 内的内存中 (VertiPaq) 引擎在每个 NUMA 节点上维护单独的作业队列。 这可确保段扫描作业运行于在其中为段数据分配内存的相同节点上。 请注意，仅在至少具有四个 NUMA 节点的系统上默认启用 NUMA 感知。 在两节点系统中，访问远程分配内存的成本通常不保证管理 NUMA 细节的开销。
-   **内存分配** - Analysis Services 已通过 Intel 线程构建模块（一种为每个内核提供单独内存池的可扩展分配器）加速。 随着内核数量的增加，系统几乎可实现线性扩展。
-   **堆碎片** - 基于 Intel TBB 的可扩展分配器还有助于缓解由于堆碎片（已证实由 Windows 堆所产生）导致的性能问题。

在大型多节点企业服务器上运行 SQL Server 2016 SP1 Analysis Services 时，性能和可伸缩性测试在查询吞吐量方面表现出了显著提升。


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>什么是 SQL Server 2016 Analysis Services 中的新增功能

虽然此版本中的大多数增强功能特定于表格模型，但对多维模型还是进行了许多改进；例如，针对 DB2 和 Oracle 等数据源的非重复计数 ROLAP 优化、Excel 2016 的钻取多重选择支持以及 Excel 查询优化。    

#### <a name="get-the-latest-tools"></a>获取最新工具
若要在此版本中充分利用所有的增强功能，请确保安装最新版本的 SSDT 和 SSMS。    
- [下载 SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [下载 SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)   

如果你有依赖于 AMO 的自定义应用程序，可能需要安装更新版本的 AMO。 有关说明，请参阅[安装 Analysis Services 数据提供程序（AMO、ADOMD.NET、MSOLAP）](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)。    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>TechNet 虚拟实验室：SQL Server 2016 Analysis Services
实践得真知？ 按照 [What's New in SQL Server 2016 Analysis Services Virtual Lab](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true)（SQL Server 2016 Analysis Services 虚拟实验室中的新增功能）逐步操作。
在此实验室中，你将创建和监视扩展事件 (xEvents)、将表格项目升级到兼容级别 1200、使用 Visual Studio 配置、实现新的计算功能、实现新的表关系功能、配置显示文件夹、管理模型翻译、使用新表格模型脚本语言 (TMSL)、使用 PowerShell 以及试用新的 DirectQuery 模式功能。

## <a name="modeling"></a>建模    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>改进了表格 1200 模型的建模性能    
对于表格 1200 模型，SSDT 中的元数据操作速度比表格 1100 或 1103 模型快得多。 相比之下，在同一硬件上，在设置为 SQL Server 2014 兼容级别 (1103) 且包含 23 个表的模型上创建关系需要 3 秒，而在设置为兼容级别 1200 的模型上创建相同的关系只需不到 1 秒。    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>为 SSDT 中的表格 1200 模型添加了项目模板    
在此版本中，你不再需要使用两个版本的 SSDT 来生成关系项目和 BI 项目。 [用于 Visual Studio 2015 的 SQL Server Data Tools](http://msdn.microsoft.com/library/mt204009.aspx) 为 Analysis Services 解决方案添加了项目模板，包括用于在 1200 兼容级别生成模型的 **Analysis Services 表格项目** 。 此外，还包括用于多维和数据挖掘解决方案的其他 Analysis Services 项目模板，但其功能级别（1100 或 1103）与以前的版本相同。    
### <a name="display-folders"></a>显示文件夹
显示文件夹现在可用于表格 1200 模型。 显示文件夹在 SQL Server Data Tools 中定义并在 Excel 或 Power BI Desktop 等客户端应用程序中呈现，可帮助你将大量的度量值组织成单独的文件夹，添加可视层次结构以方便在字段列表中导航。
### <a name="bi-directional-cross-filtering"></a>双向交叉筛选
此版本新增一项内置功能，可让你在表格模型中启用双向交叉筛选器，从而无需手动制定 DAX 解决方法来跨表关系传播筛选器上下文。 仅当能够以较高的确定性确定方向时，才自动生成筛选器。 如果跨表关系的多个查询路径的形式不明确，则不会自动创建筛选器。 有关详细信息，请参阅 [SQL Server 2016 Analysis Services 中适用于表格模型的双向交叉筛选器](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 。
 ### <a name="translations"></a>翻译    
 现在，可以将翻译的元数据存储在表格 1200 模型中。 模型中的元数据包括 **Culture**的字段、翻译的字幕和翻译的描述。 若要添加翻译，请使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“模型” > “翻译”命令。 有关详细信息，请参阅[表格模型 (Analysis Services) 中的翻译](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)。    
 ### <a name="pasted-tables"></a>粘贴的表    
 现在，当模型包含粘贴的表时，可以将 1100 或 1103 表格模型升级到 1200。 我们推荐使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]。 在 SSDT 中，将 **CompatibilityLevel** 设置为 1200，然后部署到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。 有关详细信息，请参阅 [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) 。    
 ### <a name="calculated-tables-in-ssdt"></a>SSDT 中的计算表    
*计算表* 是基于 SSDT 中 DAX 表达式或查询的仅限模型的构造。 在数据库中部署后，计算表与常规表没有区别。    

 计算表有多种用途，包括创建新表用于公开特定角色中的现有表。 典型的示例是在多个上下文中运行的日期表（订单日期、发货日期等）。 通过为给定的角色创建计算表，你可以激活表关系以便于查询，或使用计算表进行数据交互。 计算表的另一个用途是将现有表的组成部分合并到只在模型中存在的全新表。  若要了解详细信息，请参阅[创建计算表（SSAS 表格）](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md)。    
 ### <a name="formula-fixup"></a>公式修正    
 使用针对表格 1200 模型的公式修正，SSDT 可自动更新引用已重命名的列或表的任何度量值。    
 ### <a name="support-for-visual-studio-configuration-manager"></a>支持 Visual Studio 配置管理器    
 为了支持多个环境（如测试环境和预生产环境），Visual Studio 允许开发人员使用配置管理器创建多个项目配置。 多维模型已经利用此功能，但表格模型并未利用。 在此版本中，现在可以使用配置管理器部署到不同的服务器。    

## <a name="instance-management"></a>实例管理    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>在 SSMS 中管理表格 1200 模型    
 在此版本中，表格服务器模式下的 Analysis Services 实例可以运行任何兼容级别（1100、1103、1200）的表格模型。 最新的 [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) 已更新，可以显示属性并针对 1200 兼容级别的表格模型提供数据库模型管理。    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>并行处理表格模型中的多个表分区    
 此版本为包含两个或更多个分区的表提供新的并行处理功能，从而提高处理性能。 使用此功能不需要进行任何配置设置。 有关配置分区和处理表的详细信息，请参阅[表格模型分区（SSAS 表格）](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)。    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>在 SSMS 中将计算机帐户添加为管理员    
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]管理员现在可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将计算机帐户配置为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 管理员组的成员。 在“选择用户或组”对话框中，设置计算机域的“位置”，然后添加“计算机”对象类型。 有关详细信息，请参阅[向 Analysis Services 实例授予服务器管理员权限](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。    
 ### <a name="dbcc-for-analysis-services"></a>DBCC for Analysis Services    
 数据库一致性检查 (DBCC) 在内部运行，以检测数据库负载上的潜在数据损坏问题，但如果你怀疑数据或模型有问题，也可以按需运行该工具。 DBCC 将根据模型是表格式还是多维式来运行不同的检查。 有关详细信息，请参阅[适用于 Analysis Services 表格数据库和多维数据库的数据库一致性检查器 (DBCC)](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)。    
 ### <a name="extended-events-updates"></a>扩展事件更新    
 此版本在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中添加了一个图形用户界面，用于配置和管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 扩展事件。 你可以设置实时数据流来实时监视服务器活动，在内存中保持加载会话数据以加速分析，或者将数据流保存到文件以进行脱机分析。 有关详细信息，请参阅 [使用 SQL Server 扩展事件监视 Analysis Services](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 和 [Using extended events with Analysis Services (Guy in a Cube blog post and video)](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx)（在 Analysis Services 中使用扩展事件，Guy in a Cube 博客文章和视频）。    



## <a name="scripting"></a>脚本编写
 ### <a name="powershell-for-tabular-models"></a>面向表格模型的 PowerShell    
 此版本包含面向兼容级别 1200 的表格模型的 PowerShell 增强功能。 你可以使用所有适用的 cmdlet，以及特定于表格模式的 cmdlet： [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) 和 [Invoke-ProcessTable cmdlet](../analysis-services/powershell/invoke-processtable-cmdlet.md)。    
 ### <a name="ssms-scripting-database-operations"></a>SSMS 脚本数据库操作    
 在 [最新的 SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)中，现在为数据库命令（包括 Create、Alter、Delete、Backup、Restore、Attach、Detach）启用了脚本。 输出是采用 JSON 格式的表格模型脚本语言 (TMSL)。 有关详细信息，请参阅[表格模型脚本语言 (TMSL) 参考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)。    
 ### <a name="analysis-services-execute-ddl-task"></a>Analysis Services 执行 DDL 任务    
 [Analysis Services 执行 DDL 任务](../integration-services/control-flow/analysis-services-execute-ddl-task.md) 现在还接受表格模型脚本语言 (TMSL) 命令。     
 ### <a name="ssas-powershell-cmdlet"></a>SSAS PowerShell cmdlet    
 SSAS PowerShell cmdlet **Invoke-ASCmd** 现在接受表格模型脚本语言 (TMSL) 命令。 将来的版本可能会更新其他 SSAS PowerShell cmdlet，可让你使用新的表格元数据（发行说明中将标出例外情况）。    
有关详细信息，请参阅 [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) 。    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>SSMS 支持表格模型脚本语言 (TMSL)    
  使用 [最新版本的 SSMS](http://msdn.microsoft.com/library/mt238290.aspx)，你现在可以创建脚本来自动执行表格 1200 模型的大多数管理任务。 目前，可以编写以下任务的脚本：任何级别的处理任务，以及数据库级别的 CREATE、ALTER 和 DELETE。    
    
 在功能上，TMSL 相当于提供多维对象定义的 XMLA ASSL 扩展，不过，TMSL 使用 **model**、 **table**和 **relationship** 等本机描述符来描述表格元数据。 有关架构的详细信息，请参阅[表格模型脚本语言 (TMSL) 参考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)。    
    
 为表格模型生成的基于 JSON 的脚本如下所示：    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

负载是一个 JSON 文档，它可以小到如以下示例中所示，也可以大到包含整套对象定义。 [表格模型脚本语言 (TMSL) 参考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)介绍了语法。

在数据库级别，CREATE、 ALTER 和 DELETE 命令将在你熟悉的 XMLA 窗口中输出 TMSL 脚本。  还可以在此版本中编写其他命令（例如 Process）的脚本。 将来的版本可能会添加对其他许多操作的脚本支持。    

**可编写脚本的命令** | **Description**
--------------- | ----------------
创建|添加数据库、连接或分区。 ASSL 等效项为 CREATE。
createOrReplace|通过覆盖以前的版本来更新现有的对象定义（数据库、连接或分区）。 ASSL 等效于 AllowOverwrite 设置为 true 并且 ObjectDefinition 设置为 ExpandFull 时的 ALTER。
删除|删除对象定义。 ASSL 等效项为 DELETE。
refresh|处理对象。 ASSL 等效项为 PROCESS。

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>改进了 DAX 公式编辑
公式栏的更新可帮助你使用语法颜色设置来区分函数、字段和度量值，以便更轻松地编写公式，它提供智能函数和字段建议，当你的 DAX 表达式组成部分有错误时，它将使用错误 *波形曲线*来告诉你。 它还允许你换行 (Alt + Enter) 和缩进 (Tab)。 公式栏现在还允许你在度量值中编写注释，只需键入“//”，同一行上这些字符后面的所有内容将被视为注释。

### <a name="dax-variables"></a>DAX 变量    
此版本现在包含对 DAX 中变量的支持。 现在，变量可将表达式的结果存储为命名变量，然后，可以将该变量作为参数传递给其他度量值表达式。 为变量表达式计算结果值后，这些值不会更改，即使在其他表达式中引用该变量。 有关详细信息，请参阅 [VAR 函数](http://msdn.microsoft.com/library/mt243785.aspx)。    
### <a name="new-dax-functions"></a>新的 DAX 函数
在此版本中，DAX 引入了超过五十个新函数，可在 Power BI 中实现更快的计算和增强的可视化效果。 若要了解详细信息，请参阅 [新的 DAX 函数](http://msdn.microsoft.com/library/mt704075.aspx)。
### <a name="save-incomplete-measures"></a>保存未完成的度量值
现在，你可以直接在表格 1200 模型项目中保存未完成的 DAX 度量值，并在准备好继续时再次拾取这些值。
### <a name="additional-dax-enhancements"></a>其他 DAX 增强功能
- 非空计算 — 减少了非空所需的扫描次数。
- 度量值融合 — 同一表中的多个度量值将合并成单个存储引擎查询。
- 分组集 — 当查询请求多个粒度（总计/年/月）的度量值时，将在最低级别发送单个查询，其余粒度则从最低级别派生。     
- 冗余联接消除 — 向存储引擎发出的单个查询将返回维度列和度量值。
- 严格计算 IF/SWITCH — 条件为 false 的分支将不再引发存储引擎查询。 以前总是急切地计算分支，之后又将结果丢弃。     
    
## <a name="developer"></a>开发人员    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>AMO 中表格 1200 可编程性的 Microsoft.AnalysisServices.Tabular 命名空间
 Analysis Services 管理对象 (AMO) 已更新，现在包含用于管理 SQL Server 2016 Analysis Services 表格模式实例的新表格命名空间，并提供用于以编程方式创建或修改表格 1200 模型的数据定义语言。 请访问 [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) 以进一步阅读有关 API 的信息。    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Analysis Services 管理对象 (AMO) 更新
 [Analysis Services 管理对象 (AMO)](http://msdn.microsoft.com/library/mt436122.aspx) 经过重新设计，现在包含另一个程序集，即 Microsoft.AnalysisServices.Core.dll。 不管服务器模式如何，新程序集都会区分 Analysis Services 中广泛应用的常见类，如 Server、Database 和 Role。    
    
 以前，这些类是原始 Microsoft.AnalysisServices 程序集的一部分。 将它们移到新的程序集便铺平了将来扩展到 AMO 的道路，在泛型与特定于上下文的 API 之间进行分隔。    
    
 现有应用程序不受新程序集的影响。 但是，如果出于任何原因而选择使用新 AMO 程序集来重新生成应用程序，请务必添加对 Microsoft.AnalysisServices.Core 的引用。    
    
 同样，加载和调用 AMO 的 PowerShell 脚本现在必须加载 Microsoft.AnalysisServices.Core.dll。 请务必更新任何脚本。  

### <a name="json-editor-for-bim-files"></a>BIM 文件的 JSON 编辑器
Visual Studio 2015 中的代码视图现在以 JSON 格式呈现表格 1200 模型的 BIM 文件。 Visual Studio 的版本决定了是要通过内置 JSON 编辑器还是简单文本以 JSON 格式呈现 BIM 文件。

若要使用可让你展开和折叠模型各部分的 JSON 编辑器，需要安装 SQL Server Data Tools 的最新版本，以及 Visual Studio 2015（任何版本，包括免费的社区版）。 对于其他所有 SSDT 或 Visual Studio 版本，BIM 文件将以 JSON 格式呈现为简单文本。
空模型至少包含以下 JSON：

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> 避免直接编辑 JSON。 这样做可能会损坏模型。    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>MS-CSDLBI 2.0 架构中的新元素    
 以下元素已添加到 [MS-CSDLBI] 2.0 架构中定义的 **TProperty** 复杂类型：    
    
|元素|定义|    
|-------------|----------------|    
|DefaultValue|指定在评估查询时要使用的值的属性。 DefaultValue 属性是可选的，但如果无法聚合成员中的值，则会自动选择该属性。|    
|统计信息|基础数据中与列关联的一组统计信息。 这些统计信息由 TPropertyStatistics 复杂类型定义，仅当生成这些信息需要消耗大量的计算资源时才提供，如“Conceptual Schema Definition File Format with Business Intelligence Annotations”（包含业务智能标注的概述架构定义文件格式）文档的第 2.1.13.5 部分中所述。|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>新的 DirectQuery 实现    
此版本对表格 1200 模型的 DirectQuery 进行了重大改进。 总结如下：    
-   DirectQuery 现在会生成更简单的查询，从而提供更好的性能。    
-   能够以更大的力度控制对用于模型设计和测试的示例数据集的定义。    
-   DirectQuery 模式下的表格 1200 模型现在支持行级别安全性 (RLS)。 以前，RLS 会阻止在 DirectQuery 模式下部署表格模型。    
-   在 DirectQuery 模式下，表格 1200 模型现在支持计算列。 以前，计算列会阻止在 DirectQuery 模式下部署表格模型。    
-   性能优化包括针对 VertiPaq 和 DirectQuery 的冗余联接消除。 

### <a name="new-data-sources-for-directquery-mode"></a>用于 DirectQuery 模式的新数据源    
 现在支持在 DirectQuery 模式下的表格 1200年模型的数据源即包括 Oracle、 Teradata 和 Microsoft 分析平台 （以前称为并行数据仓库）。    
    
若要了解详细信息，请参阅 [DirectQuery 模式（SSAS 表格）](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。    

## <a name="see-also"></a>另请参阅
[Analysis Services 团队博客](http://blogs.msdn.microsoft.com/analysisservices/)    
[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)    
     

