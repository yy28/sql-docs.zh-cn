---
title: "创建数据驱动订阅（SSRS 教程）| Microsoft Docs"
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
caps.latest.revision: "50"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4af396aaffe116ff7000c2c787c31f775742a485
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>创建数据驱动订阅（SSRS 教程）
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 教程通过一个简单示例，介绍了如何创建数据驱动订阅，生成筛选报表输出并将其保存到文件共享，解释了数据驱动订阅的概念。 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 数据驱动订阅功能允许根据动态订阅服务器数据自定义和自动执行报表的分发。 数据驱动订阅专门用于下列情况：  
  
-   向大型收件人池分发报表，该池的成员身份可能随着分发的不同而有所变化。 例如，通过电子邮件向当前的所有客户发送月报表。  
  
-   根据预定义的条件向特定的收件人组分发报表。 例如，向组织中的所有销售经理发送销售业绩报表。
+ 自动生成各种格式的报表，例如 .xlsx 和 .pdf。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程分为三课：  
 课程 | 注释
 ------- | --------------
 [第 1 课：创建示例订阅服务器数据库](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | 在本课程中，将创建包含订阅服务器信息的本地表 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库。 用于筛选的“订单编号”信息和输出文件格式。
[第 2 课：配置报表数据源属性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) |在本课程中，将配置报表数据源属性以便能够以无人参与的方式按计划运行报表。 无人参与的处理要求存储凭据。 您还将修改报表数据集以便包括订阅服务器数据提供的参数。 此参数用于根据订单编号筛选报表数据。
 [第 3 课：定义数据驱动订阅](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | 在本课程中，将创建一个数据驱动订阅。 这一课引导您完成数据驱动订阅向导中的每一页。

 下图说明了教程的基本工作流。

步骤  |Description 
---------|---------
(1)     |  订阅配置说明了源报表、计划和映射到订阅服务器数据库的字段。        
(2)     | OrderInfo 表包含 4 个用于筛选的订单编号，每个文件 1 个。 该表还包含所生成的报告的文件格式。
(3)     | 筛选 Adventureworks 数据库中的信息，并将其返回在报表中。 
(4)     | 按 Orderinfo 表中指定的文件格式创建报表。

 
 
   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>要求  
数据驱动订阅通常由报表服务器管理员创建和维护。 创建数据驱动订阅的步骤要求具有生成查询的相关知识、了解包含订阅服务器数据的数据源，同时还要拥有对报表服务器的提升权限。  
  
本教程使用教程[创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)中创建的销售订单报表和示例数据库 AdventureWorks2014 中的数据。  
  
您的计算机必须安装以下软件才能使用此教程：  
  
-   支持数据驱动订阅的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 有关详细信息，请参阅 [SQL Server 2016 的版本和组件](../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
-   必须在本机模式下运行报表服务器。 本教程中介绍的用户界面基于本机模式报表服务器。 在 SharePoint 模式报表服务器上支持订阅，但用户界面将不同于在本教程中介绍的用户界面。  
  
-   必须运行 SQL Server 代理服务。  
  
-   包含参数的报表。 本教程以使用教程 `Sales Orders` 创建基本表报表（SSRS 教程） [创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)。  
  
-   向示例报表提供数据的 **AdventureWorks2014** 示例数据库。  
  
-   包括管理示例报表中所有订阅任务的 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 角色分配。 定义数据驱动订阅时需要执行该任务。 如果您是计算机管理员，则本地管理员的默认角色分配将提供创建数据驱动订阅所必需的权限。 有关详细信息，请参阅 [Granting Permissions on a Native Mode Report Server](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)。  
  
-   您具有写入权限的共享文件夹。 共享文件夹必须可以通过网络连接进行访问。  
  
**学完本教程的估计时间：** 30 分钟。 如果您还没有完成基本报表教程，则还需要 30 分钟。  
  
## <a name="see-also"></a>另请参阅  
[Data-Driven Subscriptions](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

