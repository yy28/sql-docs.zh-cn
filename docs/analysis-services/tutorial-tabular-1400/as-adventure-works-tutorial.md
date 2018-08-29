---
title: Analysis Services Adventure Works 教程 (1400) |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7abd968db3aacbb71ed238e3f6ae6b857c8b1d99
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084710"
---
# <a name="tabular-modeling-1400-compatibility-level"></a>表格建模（1400 兼容级别）

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

本教程提供的课程介绍如何创建和部署在表格模型[1400年兼容级别](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。 如果您熟悉 Analysis Services 和表格建模，完成本教程是了解如何创建和使用 Visual Studio 中部署基本表格模型的最快方法。 具备先决条件后，应该花费两到三个小时才能完成。  
  
## <a name="what-you-learn"></a>学习内容   
  
-   如何创建新的表格模型项目**1400年兼容级别**装有 SSDT 的 Visual Studio 中。
  
-   如何从关系数据库到表格模型项目工作区数据库导入数据。  
  
-   如何创建和管理模型中表之间的关系。  
  
-   如何创建计算的列、 度量值和关键绩效指标可帮助用户分析关键业务指标。  
  
-   如何创建和管理透视和层次结构可帮助用户更轻松地通过提供业务和特定于应用程序的视点中浏览模型数据。  
  
-   如何创建分区，以便将表数据划分为可独立于其他分区进行处理的更小逻辑部分。  
  
-   如何通过创建角色以及用户成员来保护模型对象和数据的安全。  
  
-   如何部署到的表格模型**Azure Analysis Services**服务器或**SQL Server 2017 Analysis Services**使用 SSDT 的服务器。  
  
## <a name="prerequisites"></a>必要條件  

若要完成本教程，需要：  
  
-   Azure Analysis Services 服务器或在表格模式下的 SQL Server 2017 Analysis Services 服务器。 免费注册[Azure Analysis Services 试用版](https://azure.microsoft.com/services/analysis-services/)并[创建服务器](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server)或下载免费[SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

-   [Azure SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal)与**示例 AdventureWorksDW 数据库**，或使用本地 SQL Server 数据仓库[AdventureWorksDW 示例数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 在 AdventureWorksDW 数据库安装到本地 SQL Server 数据仓库时，使用与服务器版本相对应的示例数据库版本。 

    **重要说明：** 示例数据库安装到本地 SQL Server 数据仓库，并将模型部署到 Azure Analysis Services 服务器，如果[本地数据网关](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)是必需的。

-   最新版[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 或者，如果已有 Visual Studio 2017，可以下载并安装[Microsoft Analysis Services 项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)(VSIX) 包。 对于本教程中，对 SSDT 和 Visual Studio 的引用是同义的。 

-   最新版[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。    

-   客户端应用程序，如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。 

## <a name="scenario"></a>应用场景  

本教程基于 Adventure Works Cycles，虚构公司。 Adventure Works 是对大型的跨国制造公司，生产的自行车，产品、 部件和附件的北美、 欧洲和亚洲的商业市场。 公司雇佣了 500 名工人。 此外，Adventure Works 还雇用遍布其市场群的多个区域销售团队。 你的项目将创建一个表格模型，来分析 AdventureWorksDW 数据库中的 Internet 销售数据的销售和市场营销用户。  
  
若要完成本教程，必须完成多个课程。 在每个课程中，有一些任务。 完成每个任务的顺序是必需的课程。 虽然在特定的课程中可能有多个任务的实现类似的结果，但如何完成每个任务的方式略有不同。 此方法显示了通常没有多个方法以完成一个任务，并使用已在前面的课程和任务中掌握的技能。  
  
各个课程的目的是指导使用 SSDT 中包括的功能的许多创作基本的表格模型。 因为每一课都以上一课为基础，所以，您应该按顺序完成课程。
  
本教程不提供管理在 Azure 门户中，通过使用 SSMS，或使用客户端应用程序浏览模型数据来管理服务器或数据库服务器的经验教训。 


## <a name="lessons"></a>课程  

本教程包括以下几课：  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[1-创建新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 分钟。|  
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

这些课程不是完成本教程中，所必需的但可以帮助更好地理解高级表格模型创作功能。  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 分钟。|
|[动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 分钟|
|[不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 分钟| 

  
## <a name="next-steps"></a>后续步骤  

若要开始，请参阅[第 1 课： 创建新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

