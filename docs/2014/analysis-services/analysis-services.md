---
title: SQL Server 2014 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
ms.openlocfilehash: 49258d89858c8cea3a9620f50062d6371e22ec8e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527993"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services 是在决策支持和商业智能（BI）解决方案中使用的分析数据引擎，它为商业报表和客户端应用程序（如 Excel、Reporting Services 报表和其他第三方 BI 工具）提供分析数据。 

## <a name="about-sql-server-analysis-services-documentation"></a>关于 SQL Server Analysis Services 文档

文档由版本分隔。 目前处于 SQL Server 2014 Analysis Services 文档中。

- 若要详细了解 SQL Server 2012 及更早版本，请参阅[SQL Server 以前版本的文档](https://docs.microsoft.com/previous-versions/sql/)。
- 若要了解有关 SQL Server 2014 的详细信息，请参阅[SQL Server 2014 的联机丛书](../2014-toc/index.yml)
- 若要详细了解 SQL Server 2016 及更高版本，请参阅[Analysis Services 文档](https://docs.microsoft.com/analysis-services/)。
- 若要详细了解 Azure Analysis Services，请参阅[Azure Analysis Services 文档](https://docs.microsoft.com/azure/analysis-services/)。

## <a name="analysis-services-workflow"></a>Analysis Services 工作流

典型工作流包括生成 OLAP 或表格数据模型、将模型作为数据库部署到服务器实例、处理数据库以便使用数据进行加载，然后分配权限以允许数据访问。 所有工作完成后，任何将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 作为数据源进行支持的客户端应用程序均可访问此多用途数据模型。  
  
 若要创建模型，请使用 SQL Server Data Tools （请参阅[在 Analysis Services 中使用的工具和应用程序](tools-and-applications-used-in-analysis-services.md)），并选择表格或多维和数据挖掘项目模板。 项目模板包含在模型中所需的所有对象的文件夹。 你可以使用向导来创建所有基本元素，如数据源、数据源视图、维度、多维数据集和角色。  
  
 模型由外部数据系统中的数据填充，通常是承载于 SQL Server 或 Oracle 关系数据库引擎中承载的数据仓库（表格模型支持其他数据源类型）。 模型可指定查询对象（如多维数据集），也可以指定用于多个多维数据集、计算和 KPI（封装业务逻辑）和交互（如导航和钻取行为）的维度。  
  
 若要使用模型，则将其部署到在特定服务器模式下运行数据库的服务器实例，使数据可供通过 Excel 或其他应用程序进行连接的授权用户使用。  
  
 可以在以下三种服务器模式之一中安装实例：  
  
-   作为表格实例，并运行表格模型。  
  
-   作为多维和数据挖掘实例，并运行 OLAP 多维数据集和数据挖掘模型（这是默认值）。  
  
-   作为 PowerPivot for SharePoint，并在 SharePoint 中运行 PowerPivot 和 Excel 数据模型（PowerPivot for SharePoint 是加载、查询和刷新 SharePoint 中承载的数据模型的中间层数据引擎）。  
  
 相同的数据引擎；使用数据引擎的三种不同方法。 请注意，服务器模式在安装期间设置且以后无法更改。 如果您需要其他模式，则应安装新实例。  
  
 针对 Analysis Services 的基础文档划分为多节，每一节都与您生成的项目类型相对应。 从以下链接中进行选择，以了解每种模式或功能范围的详情。  
  
 **按区域浏览内容**  
 用于[比较表格和多维解决方案 &#40;SSAS&#41;的](comparing-tabular-and-multidimensional-solutions-ssas.md)![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标")  
  
 ![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标") [Analysis Services 实例管理](instances/analysis-services-instance-management.md)  
  
 ![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标") [&#40;SSAS 表格的表格建模&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标")[多维建模 &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标")[数据挖掘 &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 [&#40;SSAS PowerPivot for SharePoint](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)的![小文件文件夹图标](../../2014/integration-services/media/filefolder-small.gif "小文件文件夹图标")&#41;  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能因版本而异。 多维和数据挖掘模型在标准版本中可用，但其功能少于更高版本。 表格模型和 PowerPivot for SharePoint 是高级功能，且在标准版本许可证中不可用。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SSAS&#41;Analysis Services 教程 &#40;](analysis-services-tutorials-ssas.md)   
 [安装 SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [开发人员指南 &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server 资源中心](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
