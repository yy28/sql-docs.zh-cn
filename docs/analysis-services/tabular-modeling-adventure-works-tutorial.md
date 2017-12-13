---
title: "表格建模 （Adventure Works 教程） |Microsoft 文档"
ms.custom: 
ms.date: 04/19/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
keywords:
- Analysis Services
- "表格模型"
- "教程"
- SSAS
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 023efa09dff09163c53259aec8ed64f3a491c807
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>表格建模（Adventure Works 教程）
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

本教程提供有关如何创建在 Analysis Services 表格模型的课程[1200年兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)使用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)，并将您的模型部署到 Analysis Services本地服务器还是在 Azure 中。  
 
如果你在使用 SQL Server 2017 或 Azure Analysis Services，并且你想要在 1400年兼容性级别创建您的模型，请使用[Azure Analysis Services-Adventure Works 教程](https://review.docs.microsoft.com/azure/analysis-services/tutorials/aas-adventure-works-tutorial?branch=master)。 此更新的版本使用新奇且现代的获取数据功能连接并导入源数据，并使用 M 语言配置分区。
 
  
## <a name="what-youll-learn"></a>学习内容   
  
-   如何在 SSDT 中创建新的表格模型项目。
  
-   如何将数据从 SQL Server 关系数据库导入表格模型项目。  
  
-   如何创建和管理模型中表之间的关系。  
  
-   如何创建和管理可帮助用户分析模型数据的计算、度量值和关键绩效指标。  
  
-   如果创建和管理透视和层次结构，通过提供业务和应用程序特定的视点，帮助用户更轻松地浏览模型数据。  
  
-   如何创建分区，以便将表数据划分为可独立于其他分区进行处理的更小逻辑部分。  
  
-   如何通过创建角色以及用户成员来保护模型对象和数据的安全。  
  
-   如何将表格模型部署到 Analysis Services 服务器上的本地或在 Azure 中。  
  
## <a name="scenario"></a>应用场景  
本教程基于 Adventure Works Cycles，虚构的公司。 Adventure Works 是大型、 跨国的制造公司，生产和分发到商业市场北美、 欧洲和亚洲的裸机和复合自行车。 与总部位于俄罗斯 Bothell，Washington，公司使用 500 的辅助进程。 此外，Adventure Works 使用多个区域的销售团队整个其市场基。  
  
为了更好地支持销售和营销团队以及高级管理人员的数据分析需要，您需要创建一个用户表格模型，以便分析 AdventureWorksDW 示例数据库中的互联网销售数据。  
  
为了完成本教程和 Adventure Works 互联网销售表格模型，您必须完成一系列课程。 每个课程中有大量的任务；按顺序完成每项任务对于完成这一课是必不可少的。 在特定课中可能有多个任务完成的类似的结果，但如何完成每个任务却略有不同。 这是为了显示是通常用于完成特定任务，并为质询你通过使用您在前面的任务中学的技能的多个方法。  
  
这些课程旨在指导你完成创作基本表格模型使用许多 SSDT 中包括的功能在内存中模式中运行。 因为每一课都以上一课为基础，所以，您应该按顺序完成课程。 一旦你已完成的所有课程，你将已编写并部署 Analysis Services 服务器上的 Adventure Works Internet Sales 示例表格模型。  
  
本教程并未提供有关以下内容的课程或信息：通过使用 SQL Server Management Studio 管理已部署的表格模型数据库，或者使用报表客户端应用程序连接到已部署的模型以浏览模型数据。  
  
## <a name="prerequisites"></a>先决条件  
若要完成本教程，你将需要以下先决条件：  
  
-   最新版本的 [！包括[ssBIDevStudioFull](../ssdt/download-sql-server-data-tools-ssdt.md)。

-   SQL Server Management Studio 最新版本。 [获取最新版本](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 
  
-   客户端应用程序，如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或[!INCLUDE[msCoName](../includes/msconame-md.md)]Excel。    
  
-   具有 Adventure Works DW 2014 示例数据库的 SQL Server 实例。 此示例数据库包括完成本教程所需的数据。 [获取最新版本](http://go.microsoft.com/fwlink/?LinkID=335807)。  
  

-   Azure Analysis Services 或 SQL Server 2016 或更高版本的 Analysis Services 实例部署到您的模型。 [注册一个免费的 Azure Analysis Services 试用版](https://azure.microsoft.com/services/analysis-services/)。
  
## <a name="lessons"></a>课程  
本教程包括以下几课：  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 分钟。|  
|[第 2 课：添加数据](../analysis-services/lesson-2-add-data.md)|20 分钟|  
|[第 3 课：标记为日期表](../analysis-services/lesson-3-mark-as-date-table.md)|3 分钟|  
|[第 4 课： 创建关系](../analysis-services/lesson-4-create-relationships.md)|10 分钟。|  
|[第 5 课： 创建计算的列](../analysis-services/lesson-5-create-calculated-columns.md)|15 分钟|
|[第 6 课： 创建度量值](../analysis-services/lesson-6-create-measures.md)|30 分钟|  
|[第 7 课：创建关键绩效指标](../analysis-services/lesson-7-create-key-performance-indicators.md)|15 分钟|  
|[第 8 课： 创建透视](../analysis-services/lesson-8-create-perspectives.md)|5 分钟|  
|[Lesson 9： 创建层次结构](../analysis-services/lesson-9-create-hierarchies.md)|20 分钟|  
|[第 10 课： 创建分区](../analysis-services/lesson-10-create-partitions.md)|15 分钟|  
|[第 11 课： 创建角色](../analysis-services/lesson-11-create-roles.md)|15 分钟|  
|[第 12 课：在 Excel 中分析](../analysis-services/lesson-12-analyze-in-excel.md)|20 分钟| 
|[第 13 课：部署](../analysis-services/lesson-13-deploy.md)|5 分钟|  
  
## <a name="supplemental-lessons"></a>补充课程  
本教程还包括 [补充课程](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e)。 这一节中的主题不是完成本教程所必需的，但对于更好地了解高级表格模型创作功能会很有帮助。  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[通过使用行筛选器实现动态安全性](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 分钟|  

  
## <a name="next-step"></a>下一步  
若要开始学习本教程，请继续第一课： [第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

