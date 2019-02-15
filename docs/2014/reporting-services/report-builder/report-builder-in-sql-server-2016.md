---
title: SQL Server 2014 中的报表生成器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: eb8120b9ba413ce6f1a59667c136b1580eb5b675
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290435"
---
# <a name="report-builder-in-sql-server-2014"></a>SQL Server 2014 中的报表生成器
  Report Builder 是一种报表创作环境，适用于喜欢在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office 环境下工作的业务用户。 设计报表时，您可以指定在何处获取数据、获取哪些数据以及如何显示数据。 当您运行报表时，报表处理器将获取您已经指定的所有信息，检索数据，并将数据与报表布局进行组合以生成报表。 您可以在报表生成器中预览报表，也可以将报表发布到报表服务器或处于 SharePoint 集成模式下的报表服务器，让其他人可以运行它。  
  
 本图中的报表包含一个矩阵，带有行组和列组、迷你图、指示器，以及角单元中的摘要饼图，还附带一个地图，有两组地理数据，以颜色和圆圈大小表示。  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="JumpStartReptCreation"></a> 快速开始报表创建  
  
-   **开始将报表 withreport 部件**由你的团队中的其他人创建的。 报表部件是已单独发布到报表服务器或与报表服务器集成的 SharePoint 站点上的报表项。 它们可以在其他报表中重用。 表、矩阵、图表和图像等报表项可以作为报表部件发布。  
  
-   **共享数据集开始**由你的团队中的其他人创建的。 共享数据集是基于保存到报表服务器或与报表服务器集成的 SharePoint 站点上的共享数据源的查询。  
  
-   **使用表、矩阵或图表向导创建报表**。 选择数据源连接，拖放字段以创建数据集查询，选择布局和样式并自定义报表。  
  
-   **使用地图向导** 创建显示针对地理或几何背景的聚合数据的报表。 地图数据可以是来自 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询或 Environmental Systems Research Institute, Inc.(ESRI) 形状文件的空间数据。 还可以添加 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing 地图图块背景。  
  

  
##  <a name="DesignRept"></a> 设计报表  
  
-   **创建具有表、 矩阵、 图表和自由格式报表布局的报表。** 为基于列的数据创建表报表，为汇总数据创建矩阵报表（如交叉表或数据透视表），为图形数据创建图表报表，为任何其他类型的数据创建自由格式报表。 报表可以与基于 Web 的动态应用程序的列表、图形和控件一同嵌入其他报表和图表。  
  
-   **可基于各种数据源生成报表。** 使用具有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]托管数据提供程序、OLE DB 提供程序或 ODBC 数据源的任何数据源类型的数据生成报表。 可以创建使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、Oracle、Hyperion 及其他数据库中的关系数据和多维数据的报表。 您可以使用 XML 数据处理扩展插件从任何 XML 数据源检索数据。 可以使用表值函数来设计自定义数据源。  
  
-   **修改现有报表。** 通过使用报表生成器，您可以自定义和更新中创建的报表[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]报表设计器。  
  
-   **修改数据**通过筛选、 分组和排序数据，或通过添加公式或表达式。  
  
-   **添加图表、仪表、迷你图和指示器** ，以直观的形式汇总数据，使大量聚合信息一目了然。  
  
-   **添加交互功能** ，如文档结构图、显示/隐藏按钮以及指向子报表和钻取报表的钻取链接。 使用参数和筛选器可以筛选自定义视图的数据。  
  
-   **嵌入或引用图像** 以及其他资源，包括外部内容。  
  

  
##  <a name="ManageRpt"></a> 管理报表  
  
-   **将报表的定义保存到** 计算机或报表服务器，您可以在其中管理报表定义，还可以与他人共享。  
  
-   **选择显示格式** ，可以在打开报表时选择，也可以在打开报表后选择。 您可以选择面向 Web 的格式、面向页的格式及桌面应用程序格式。 这些格式包括 HTML、MHTML、PDF、XML、CSV、TIFF、Word 和 Excel。  
  
-   **设置订阅。** 在将报表发布到报表服务器或处于 SharePoint 集成模式下的报表服务器之后，您可以将报表配置为在特定时间运行、创建报表历史记录并设置电子邮件订阅。  
  
-   **生成数据馈送** ，使用 Reporting Services Atom 呈现扩展插件从报表生成数据馈送。  
  
> [!NOTE]  
>  发布的报表存储在报表服务器或处于 SharePoint 集成模式下的报表服务器上，由报表服务器管理员进行管理。 报表服务器管理员可以定义安全性、设置属性并计划报表历史记录和电子邮件报表传递等操作。 他们可以创建共享计划和共享数据源，供常规使用。 管理员还管理所有报表服务器文件夹。 执行管理任务的能力取决于用户权限。  
  

  
##  <a name="InThisSection"></a> 本节内容  
 [SQL Server 2014 的报表生成器中的新增功能](../what-s-new-in-report-builder-for-sql-server-2014.md)  
 介绍此版本的报表生成器的新增功能，包括地图。  
  
 [教程：创建快速图表报表脱机](tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 介绍报表生成器以及可用来帮助创建报表的向导。 教程提供了一组供您使用的数据，因此不需要连接到数据源即可开始工作。  
  
 [规划报表（报表生成器）](../report-design/planning-a-report-report-builder.md)  
 提供在开始生成报表之前应当考虑哪些情况的信息。  
  
 [报表创作概念（报表生成器和 SSRS）](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 定义在整个报表生成器文档中使用的主要概念。  
  
 [报表设计视图（报表生成器）](report-design-view-report-builder.md)  
 介绍报表设计视图的不同窗格和区域。  
  
 [共享数据集设计视图（报表生成器）](shared-dataset-design-view-report-builder.md)  
 介绍共享数据集设计视图的不同窗格和区域。  
  
 [键盘快捷键（报表生成器）](keyboard-shortcuts-report-builder.md)  
 概述可用于在报表生成器中导航和设计报表的快捷键。  
  
 [启动报表生成器&#40;报表生成器&#41;](start-report-builder.md)  
 说明如何启动报表生成器的两个不同版本：独立和 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]。  
  
  
