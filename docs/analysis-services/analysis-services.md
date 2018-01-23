---
title: "Analysis Services |Microsoft 文档"
ms.date: 05/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: "60"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 00b88b320118df9649b546b35259ec1c8acdc7cf
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="what-is-analysis-services"></a>什么是 Analysis Services？
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services 是决策支持和业务分析，Reporting Services 报表，为业务报告和客户端应用程序，例如 Power BI 中，Excel 中，提供的分析数据和其他数据可视化工具中使用的分析数据引擎。  
  
 典型的工作流包括创作多维或表格数据模型中，将模型作为在本地 SQL Server Analysis Services 或 Azure Analysis Services 服务器实例的数据库部署、 设置重复的数据处理和分配若要允许最终用户通过数据访问的权限。 准备就绪时，可以通过任何支持作为数据源的 Analysis Services 的客户端应用程序访问你的语义的数据模型。  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>本地和云中的 Analysis Services
Analysis Services 现已作为一项 Azure 服务在云中推出。 Azure Analysis Services 支持 1200年或更高的兼容性级别的表格模型。 可支持 DirectQuery、分区、行级安全性、双向关系和翻译。 若要了解详细信息并免费试用，请参阅 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)。 
  
## <a name="server-mode"></a>服务器模式  
 在安装 Analysis Services 使用 SQL Server 安装程序时，在配置期间指定为该实例的服务器模式。  每种模式都包含特定 Analysis Services 解决方案所独有的不同功能。   
  
-   **表格模式下**-实现内存中关系数据建模构造 （模型、 表、 列、 度量值、 层次结构）。  

-   **多维和数据挖掘模式** - 实现 OLAP 建模构造（多维数据集、维度、度量值）。 

-   **Power Pivot 模式下**-SharePoint 中的实现 Power Pivot 和 Excel 数据模型 （Power Pivot for SharePoint 是一个中间层数据引擎，加载、 查询和刷新在 SharePoint 中托管的数据模型）。  
  
 单个实例只能使用一种模式进行配置，并且以后无法更改。  可以在同一服务器上安装具有不同模式的多个实例，但是需要运行安装程序并为每个实例指定配置设置。 有关详细的信息和在每种模式中提供的不同功能的比较，请参阅[比较表格和多维解决方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)。
  
## <a name="authoring-and-managing-solutions"></a>创作和管理解决方案  
 若要创建模型，并将其部署到服务器，你可以使用 SQL Server Data Tools，选择是表格或多维和数据挖掘项目模板。 项目模板包含在模型中所需的所有对象的文件夹。 向导和设计器可帮助你创建许多例如连接到数据源、 关系、 度量值和角色的基本元素。 一旦你的模型数据库部署到服务器中，使用 SQL Server Management Studio (SSMS) 来配置数据处理、 监视和管理服务器和数据库。 若要了解详细信息，请参阅[工具和 Analysis Services 中使用的应用程序](../analysis-services/tools-and-applications-used-in-analysis-services.md)。 
  
## <a name="documentation-by-area"></a>文档（按区域）  
在常规 Azure 文档包含了 Azure Analysis Services 的文档。 而且，SQL Server Analysis Services 的文档包含与 SQL 文档。 但是，至少对于表格模型中，如何创建和部署你的项目是无论你使用何种平台大致相同。  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [什么是 SQL Server Analysis Services 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)   
*  [比较表格和多维解决方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [表格模型](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [多维模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [数据挖掘](../analysis-services/data-mining/data-mining-ssas.md)  
*  [Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [实例管理](../analysis-services/instances/analysis-services-instance-management.md)    
*  [教程](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [开发人员文档](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [技术参考 (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)
