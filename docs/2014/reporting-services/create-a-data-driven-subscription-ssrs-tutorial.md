---
title: 创建数据驱动订阅（SSRS 教程）| Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f4122aa579766d80cfac6600753d4a8f8a672ae9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017909"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>创建数据驱动订阅（SSRS 教程）
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供数据驱动订阅功能，这样您便可根据动态订阅服务器数据自定义报表的分发。 数据驱动订阅专门用于下列情况：  
  
-   向大型收件人池分发报表，该池的成员身份可能随着分发的不同而有所变化。 例如，向当前的所有客户分发月报表。  
  
-   根据预定义的条件向特定的收件人组分发报表。 例如，向某个组织中的前十位销售经理分发销售业绩报表。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程通过简单的示例对概念进行解释，为您演示如何使用数据驱动订阅。  
  
 本教程分为三课：  
  
 [第 1 课：创建示例订阅服务器数据库](lesson-1-creating-a-sample-subscriber-database.md)  
 在这一课中，您将学习如何创建包含订阅服务器信息的本地 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库。  
  
 [第 2 课：修改报表数据源属性](lesson-2-modifying-the-report-data-source-properties.md)  
 在这一课中，您将学习如何修改报表数据源属性以便能够以无人参与的方式运行报表。 无人参与的处理要求存储凭据。 您还将修改报表数据集以便包括订阅服务器数据提供的参数。  
  
 [第 3 课：定义数据驱动订阅](lesson-3-defining-a-data-driven-subscription.md)  
 在这一课中，您将学习如何定义数据驱动订阅。 这一课引导您完成数据驱动订阅向导中的每一页。  
  
## <a name="requirements"></a>要求  
 数据驱动订阅通常由报表服务器管理员创建和维护。 要创建数据驱动订阅，必须要具备生成查询的专业技术，了解包含订阅服务器数据的数据源，同时还要拥有对报表服务器的提升权限。  
  
 本教程将使用在本教程中创建的报表[创建基本表报表&#40;SSRS 教程&#41;](create-a-basic-table-report-ssrs-tutorial.md)和中的数据 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 若要使用本教程，您的系统必须安装以下组件：  
  
-   支持数据驱动订阅的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 有关详细信息，请参阅[各版本和 SQL Server 2014 的组件](../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
-   必须在本机模式下运行报表服务器。 本教程中介绍的用户界面基于本机模式报表服务器。 在 SharePoint 模式报表服务器上支持订阅，但用户界面将不同于在本教程中介绍的用户界面。  
  
-   必须运行 SQL Server 代理服务。  
  
-   包含参数的报表。 本教程以使用教程 `Sales Orders` 创建基本表报表（SSRS 教程） [创建基本表报表（SSRS 教程）](create-a-basic-table-report-ssrs-tutorial.md)。  
  
-   向示例报表提供数据的 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 示例数据库。  
  
-   包括管理同一个示例报表中所有订阅任务的角色分配。 定义数据驱动订阅时需要执行该任务。 如果您是计算机管理员，则本地管理员的默认角色分配将提供创建数据驱动订阅所必需的权限。 有关详细信息，请参阅 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)。  
  
-   您具有写入权限的共享文件夹。 共享文件夹必须可以通过网络连接进行访问。  
  
 **学完本教程的估计时间：** 30 分钟。 如果您还没有完成基本报表教程，则还需要 30 分钟。  
  
## <a name="see-also"></a>请参阅  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [创建基本表报表（SSRS 教程）](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
