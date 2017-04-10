---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, 关于 Analysis Services - 多维数据"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, 关于 Analysis Services - 多维数据"
  - "SQL Server Analysis Services"
  - "多维数据 [Analysis Services]"
  - "SSAS, 关于 Analysis Services - 多维数据"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 是在决策支持和商业分析中使用的联机分析数据引擎，它为商业报表和客户端应用程序（如 Power BI、Excel、Reporting Services 报表和其他数据可视化工具）提供分析数据。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的典型工作流包括创作多维或表格数据模型、将模型作为数据库部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例、对数据库进行处理以向其加载数据或元数据、设置数据刷新，以及分配权限以允许最终用户进行数据访问。 所有工作完成后，任何支持将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 作为数据源的客户端应用程序均可访问此多用途语义数据模型。  
  
 模型由外部数据系统中的数据填充，通常是承载于 SQL Server 或 Oracle 关系数据库引擎中承载的数据仓库（表格模型支持其他数据源类型）。 模型可指定查询对象（如多维数据集），也可以指定用于多个多维数据集、计算和 KPI（封装业务逻辑）和交互（如导航和钻取行为）的维度。  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>本地和云中的 Analysis Services
Analysis Services 现已作为一项 Azure 服务在云中推出。 当前还处于预览状态，Azure Analysis Services 支持 1200 兼容级别的表格模型。 可支持 DirectQuery、分区、行级安全性、双向关系和翻译。 若要了解详细信息并免费试用，请参阅 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)。 
  
## <a name="server-mode"></a>服务器模式  
 使用 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 安装程序安装 Analysis Services 时，在配置过程中可为该实例指定服务器模式。  每种模式都包含特定 Analysis Services 解决方案所独有的不同功能。  
  
-   **多维和数据挖掘模式** - 实现 OLAP 建模构造（多维数据集、维度、度量值）。  
  
-   **表格模式** - 实现内存中关系数据建模构造（模型、表、列）。  
  
     可以使用最新功能在默认兼容级别 1200 创建表格模型，也可在较旧的 1103 兼容级别创建。 各个兼容级别之间存在显著差异。 若要了解如何比较各级别的差异，请参阅 [Analysis Services 中表格模型的兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
-   **Power Pivot 模式** - 在 SharePoint 中实现 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 和 Excel 数据模型（[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 是加载、查询和刷新 SharePoint 中承载的数据模型的中间层数据引擎）。  
  
 单个实例只能使用一种模式进行配置，并且以后无法更改。  可以在同一服务器上安装具有不同模式的多个实例，但是需要运行安装程序并为每个实例指定配置设置。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能因版本而异。 有关详细信息，请参阅 [SQL Server 2016 的各版本和支持的功能](../sql-server/sql-server-2016-的各版本和支持的功能.md) 
  
## <a name="authoring-solutions"></a>创作解决方案  
 若要创建模型，请使用 SQL Server Data Tools（请参阅 [在 Analysis Services 中使用的工具和应用程序](../analysis-services/tools-and-applications-used-in-analysis-services.md)），并选择表格或多维和数据挖掘项目模板。 项目模板包含在模型中所需的所有对象的文件夹。 向导可帮助创建许多基本元素，如数据源、数据源视图、维度、多维数据集和角色。  
  
## <a name="documentation-by-area"></a>文档（按区域）  
针对 Analysis Services 的文档划分为多节，每一节都与生成的项目类型相对应。 从以下链接中进行选择，以了解每种模式或功能范围的详情。  
   
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[新增功能](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[比较表格和多维解决方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[表格模型](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[多维模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[数据挖掘](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标") [Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标") [Analysis Services 实例管理](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标") [Analysis Services 教程](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标") [Analysis Services Developer Documentation](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)（Analysis Services 开发人员文档）  
 
![小文件夹图标](../analysis-services/media/filefolder-small.png "小文件夹图标")[技术参考 (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)