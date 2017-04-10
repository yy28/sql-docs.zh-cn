---
title: "表格建模（Adventure Works 教程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
keywords: 
  - "Analysis Services"
  - "表格模型"
  - "教程"
  - "SSAS"
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# 表格建模（Adventure Works 教程）
本教程提供的课程介绍如何通过使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services 表格模型。  
  
  
## 学习内容  
在本教程的课程中，您将掌握以下内容：  
  
-   如何在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中创建新的表格模型项目  
  
-   如何将数据从 SQL Server 关系数据库导入表格模型项目。  
  
-   如何创建和管理模型中表之间的关系。  
  
-   如何创建和管理可帮助用户分析模型数据的计算、度量值和关键绩效指标。  
  
-   如果创建和管理透视和层次结构，通过提供业务和应用程序特定的视点，帮助用户更轻松地浏览模型数据。  
  
-   如何创建分区，以便将表数据划分为可独立于其他分区进行处理的更小逻辑部分。  
  
-   如何通过创建角色以及用户成员来保护模型对象和数据的安全。  
  
-   如何将表格模型部署到在表格模式下运行的 Analysis Services 的沙盒或生产实例中。  
  
## 应用场景  
本教程基于 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]，这是一家虚构的公司。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨国制造公司，生产金属复合材料的自行车，产品远销北美、欧洲和亚洲市场。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 公司总部设在华盛顿州的伯瑟尔市，雇佣了 500 名工人。 此外，在 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 市场中还活跃着一些地区销售团队。  
  
为了更好地支持销售和营销团队以及高级管理人员的数据分析需要，您需要创建一个用户表格模型，以便分析 AdventureWorksDW 示例数据库中的互联网销售数据。  
  
为了完成本教程和 Adventure Works 互联网销售表格模型，您必须完成一系列课程。 每个课程中有大量的任务；按顺序完成每项任务对于完成这一课是必不可少的。 虽然在特定的课程中可能有多个任务可获得类似结果；但您完成每项任务的方式稍有不同。 也就是说，可以通过多种方法完成某个特定任务，并通过使用先前任务中掌握的技能来向您提问。  
  
这些课程的目的是引导您完成以下过程：通过使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中包含的多项功能创作在内存中模式下运行的基本表格模型。 因为每一课都以上一课为基础，所以，您应该按顺序完成课程。 在完成所有课程之后，您就已经在 Analysis Services 服务器上创作和部署了 Adventure Works 互联网销售示例表格模型。  
  
本教程并未提供有关以下内容的课程或信息：通过使用 SQL Server Management Studio 管理已部署的表格模型数据库，或者使用报表客户端应用程序连接到已部署的模型以浏览模型数据。  
  
## 先决条件  
为了完成本教程，您必须安装了以下必备组件：  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在表格模式下运行的 Analysis Services 实例。  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 [获取最新版本。](https://msdn.microsoft.com/library/mt204009.aspx)  
  
-   Adventure Works DW 2014 示例数据库。 此示例数据库包括完成本教程所需的数据。 若要下载示例数据库，请转到 [http://go.microsoft.com/fwlink/?LinkID=335807](http://go.microsoft.com/fwlink/?LinkID=335807)。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 或更高版本（与第 11 课中的“在 Excel 中分析”功能结合使用）。  
  
## 课程  
本教程包括以下几课：  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 分钟。|  
|[第 2 课：添加数据](../analysis-services/lesson-2-add-data.md)|20 分钟|  
|[第 3 课：重命名列](../analysis-services/lesson-3-rename-columns.md)|20 分钟|  
|[第 4 课：标记为日期表](../analysis-services/lesson-4-mark-as-date-table.md)|3 分钟|  
|[第 5 课：创建关系](../analysis-services/lesson-5-create-relationships.md)|10 分钟。|  
|[第 6 课：创建计算列](../analysis-services/lesson-6-create-calculated-columns.md)|15 分钟|  
|[第 7 课：创建度量值](../analysis-services/lesson-7-create-measures.md)|30 分钟|  
|[第 8 课：创建关键绩效指标](../analysis-services/lesson-8-create-key-performance-indicators.md)|15 分钟|  
|[第 9 课：创建透视](../Topic/Lesson%209:%20Create%20Perspectives.md)|5 分钟|  
|[第 10 课：创建层次结构](../analysis-services/lesson-10-create-hierarchies.md)|20 分钟|  
|[第 11 课：创建分区](../analysis-services/lesson-11-create-partitions.md)|15 分钟|  
|[第 12 课：创建角色](../analysis-services/lesson-12-create-roles.md)|15 分钟|  
|[第 13 课：在 Excel 中分析](../analysis-services/lesson-13-analyze-in-excel.md)|20 分钟|  
|[第 14 课：部署](../analysis-services/lesson-14-deploy.md)|5 分钟|  
  
## 补充课程  
本教程还包括[补充课程](../Topic/Supplemental%20Lessons.md)。 这一节中的主题不是完成本教程所必需的，但对于更好地了解高级表格模型创作功能会很有帮助。  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[通过使用行筛选器实现动态安全性](../analysis-services/implement-dynamic-security-by-using-row-filters.md)|30 分钟|  
|[为 Power View 报表配置报表属性](../analysis-services/configure-reporting-properties-for-power-view-reports.md)|30 分钟|  
  
## 下一步  
若要开始学习本教程，请继续第一课：[第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  
