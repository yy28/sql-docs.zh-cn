---
title: 通过使用 Power BI (SQL Server 数据 Migration Assistant) 报告上合并评估 |Microsoft 文档
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f3ed0802a0a7570109bdae99151c8c6ce4fa01
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>报告合并评估使用 Power BI （数据迁移助手）

本文介绍如何创建用于合并的迁移评估的 Power BI 报表。

有关通过使用数据迁移助手整合迁移评估的信息，请参阅[合并评估报表](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>示例 Power BI 报表

你可以从这下载的合并的迁移评估的 Power BI 报表示例[Github 存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)。

以下报表可以包含： 

- [仪表板](#dashboard--details)

  包括快照统计信息和深化报表。

- [在本地升级准备情况](#on-premises-upgrade-readiness--details)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报表显示你评估数据库的百分比升级成功。

- [在本地功能奇偶校验](#on-premise-feature-parity--details)

  显示目标 SQL Server 版本的功能建议。

- [Azure SQL DB 升级准备情况](#azure-sql-db-upgrade-readiness--details)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报表显示针对 Azure SQL DB 迁移评估的数据库的百分比升级成功。

- [Azure SQL 数据库不受支持的功能](#azure-sql-db-unsupported-features--details)

  显示现有数据库不支持在 Azure SQL DB 中 (V12) 中的功能。

你可以修改这些报表能够通过更改 Power BI 中的数据源使用你的环境。 

1. 选择向下箭头旁边**编辑查询**，然后选择**数据源设置**。

   ![编辑查询菜单上，数据源设置](../dma/media/DataSourceSettings.png)

1. 选择**更改源...**，并输入的服务器和数据库的值。

   ![更改源、 服务器和数据库](../dma/media/ChangeSource.png)

1. 选择**确定**，然后选择**关闭**。

1. 刷新您的报表。

   ![刷新 Power BI 报表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>仪表板报表

![仪表板报表](../dma/media/DashboardReport.png)

仪表板显示有关所有你评估的详细信息。 可以使用左侧切片器要作为筛选依据实例或数据库。 条形图可用于向下钻取以查看哪里问题的特定类别。

若要向下钻取，选择与条形图的右上角的向下箭头的圆圈。

![类别明细](../dma/media/CategoryDrillDown.png)

下图中所示设置明细序列 (下**轴**)。 若要更改序列，拖动到所需顺序的列。

![条形图轴的可视化效果](../dma/media/VisualizationsAxis.png)

在第一次筛选由特定数据库，然后深化到特定类别问题时，此视图将变得更加强大。 在下面的示例中，例如选择了 HR 数据库**SQL01**查看阻止 （重大更改） 的迁移的所有对象。

![重大 HR 数据库的更改](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>在本地升级准备情况报告

![在本地升级准备情况报告](../dma/media/OnPremisesUpgradeReadinessReport.png)

此报表显示如何准备你的数据库要迁移到更高版本的 SQL Server 的快照。 此报表中的数据来自 dbo。UpgradeSuccessFactor\_DMAReporting 数据库中的 OnPrem 视图。

按实例和数据库名称筛选和评分卡使用顶部，你可以查看哪些可能太迁移数据库的版本。 例如，如果通过 AdventureWorks 2012 数据库筛选时，你可以看到数据库已准备好将移到报表中列出的所有 SQL Server 版本。 这确定通过确保没有为该数据库和兼容性级别的重大更改。

![升级成功 AdventureWorks 数据库的因素](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>在本地功能奇偶校验报表

![在本地功能奇偶校验报表](../dma/media/OnPremisesFeatureParityReport.png)

使用此报表以突出显示可用于目标 SQL Server 版本中的数据库的新功能。

在漏斗图中选择一项功能，突出显示了在底部的数据，该功能受影响的对象。 在下面的示例中，**节省的存储空间的 Stretch database**选择功能，并列出表，无法受益于此功能。

![适用于 Stretch Database 的功能建议](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 升级准备情况报表

![Azure SQL DB 升级准备情况报表](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此报表显示数据库准备将迁移到 Azure SQL 数据库 V12。 此报表中的数据来自 dbo。UpgradeSuccessRanking DMAReporting 数据库中的视图。

### <a name="azure-features-parity-report"></a>Azure 功能奇偶校验报表

![Azure 功能奇偶校验报表](../dma/media/AzureFeaturesParityReport.png)

使用此报表以突出显示*实例级别功能*不受 Azure SQL 数据库 V12。

当在漏斗图中选择一项功能时，在底部的数据列出的实例和不支持的数据库功能。 在下面的示例中，选择此功能： **Azure SQL 数据库中不支持始终打开可用性组配置**。  

![始终打开可用性组功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL 数据库不受支持的功能报表

![Azure SQL 数据库不受支持的功能报表](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

此报表突出显示的功能不支持给定**数据库**当目标是 Azure SQL 数据库 (V12)。

通过筛选漏斗图中的数据库名称和功能值，可以在不受支持的功能来查看详细信息。 详细信息包括的对象会受到影响和解决问题的建议。

例如，筛选 DTC 数据库和**无法升级只读数据库**，你可以看到的受影响的对象的列表。

![只读数据库不能为升级问题](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另请参阅

[数据迁移助手的概述](../dma/dma-overview.md)

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下载](https://powerbi.microsoft.com/)
