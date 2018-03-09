---
title: "Analysis Services Adventure Works 教程 (1400) |Microsoft 文档"
description: "为 Analysis Services 引入了 Adventure Works 教程"
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 8a7511c096ffacf249187c9f45d71bca340bb1ca
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-modeling-1400-compatibility-level"></a>表格建模 （1400年兼容性级别）

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

本教程提供有关如何创建和部署表格模型在课程[1400年兼容性级别](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。 如果你熟悉 Analysis Services 和表格建模，完成本教程是学习如何创建和使用 Visual Studio 中部署基本的表格模型的最快方法。 一旦你准备先决条件就地，它应需要两至三个小时才能完成。  
  
## <a name="what-you-learn"></a>你掌握的内容   
  
-   如何创建在新的表格模型项目**1400年兼容性级别**使用 SSDT 的 Visual Studio 中。
  
-   如何将数据从关系数据库导入表格模型项目工作区数据库。  
  
-   如何创建和管理模型中表之间的关系。  
  
-   如何创建计算的列、 度量值和关键绩效指标可帮助用户分析关键业务度量值。  
  
-   如何创建和管理透视和帮助用户更轻松地通过提供业务和应用程序特定视点中浏览模型数据的层次结构。  
  
-   如何创建分区，以便将表数据划分为可独立于其他分区进行处理的更小逻辑部分。  
  
-   如何通过创建角色以及用户成员来保护模型对象和数据的安全。  
  
-   如何部署到表格模型**Azure Analysis Services**服务器或**SQL Server 自 2017 年 Analysis Services**使用 SSDT 的服务器。  
  
## <a name="prerequisites"></a>必要條件  

若要完成本教程，你需要：  
  
-   Azure Analysis Services 服务器或在表格模式下的 SQL Server 自 2017 年 Analysis Services 服务器。 注册免费的[Azure Analysis Services 试用版](https://azure.microsoft.com/services/analysis-services/)和[创建服务器](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server)或下载免费[SQL Server 自 2017 年 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

-   [Azure SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal)与**示例 AdventureWorksDW 数据库**，或使用本地 SQL Server 数据仓库[AdventureWorksDW 示例数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 在安装到本地 SQL Server 数据仓库时 AdventureWorksDW 数据库，使用您的服务器版本相对应的示例数据库版本。 

    **重要说明：**将示例数据库安装到本地 SQL Server 数据仓库，并将您的模型部署到 Azure Analysis Services 服务器，如果[本地数据网关](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)是必需的。

-   最新版本[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 或者，如果你已有 Visual Studio 2017，你可以下载并安装[Microsoft Analysis Services 项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)(VSIX) 包。 本教程中，对 SSDT 和 Visual Studio 的引用是同义词。 

-   最新版本[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。    

-   客户端应用程序，如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。 

## <a name="scenario"></a>应用场景  

本教程基于 Adventure Works Cycles，虚构的公司。 Adventure Works 是一大、 跨国制造公司，生产和分发自行车、 部件和商业市场北美、 欧洲和亚洲的附件。 公司采用 500 的辅助进程。 此外，Adventure Works 使用多个区域的销售团队整个其市场基。 你的项目是创建销售和市场营销用户来分析 AdventureWorksDW 数据库中的 Internet 销售数据的表格模型。  
  
若要完成本教程，你必须完成各种课程。 在每个课程中，有一些任务。 完成顺序每个任务是所需完成本课程。 在特定课中可能有多个任务完成的类似的结果，但如何完成每个任务却略有不同。 此方法显示通常没有完成任务，并为质询你通过使用您在前面的课程中和任务中学到的技能的多个方法。  
  
这些课程旨在指导你完成通过使用 SSDT 中包括的功能的许多创作一个基本的表格模型。 因为每一课都以上一课为基础，所以，您应该按顺序完成课程。
  
本教程不提供有关管理在 Azure 门户中，通过使用 SSMS，或使用客户端应用程序来浏览模型数据管理服务器或数据库的服务器的课程。 


## <a name="lessons"></a>课程  

本教程包括以下几课：  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[1-创建一个新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 分钟。|  
|[2 - 获取数据](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 分钟。|  
|[3 - 标记为日期表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 分钟|  
|[4 - 创建关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 分钟。|  
|[5 - 创建计算列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 分钟|
|[6 - 创建度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 分钟|  
|[7-创建关键绩效指标 (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 分钟|  
|[8 - 创建透视](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 分钟|  
|[9 - 创建层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 分钟|  
|[10 - 创建分区](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 分钟|  
|[11 - 创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 分钟|  
|[12 - 在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 分钟| 
|[13 - 部署](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 分钟|  
  
## <a name="supplemental-lessons"></a>补充课程  

这些课程不需要完成本教程中，但在更好地了解高级表格模型创建功能非常有用。  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 分钟。|
|[动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 分钟|
|[不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 分钟| 

  
## <a name="next-steps"></a>后续步骤  

若要开始，请参阅[第 1 课： 创建新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

