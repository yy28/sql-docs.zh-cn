---
title: 分析合并的数据迁移助手的评估报告使用 Power BI (SQL Server) |Microsoft Docs
description: 了解如何使用 Power BI 来分析您已导入和合并到 SQL Server 中的数据迁移评估报表
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 786e86fb6f0326e2f8ea568f4c069828ff1ff4c6
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57974116"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>分析创建的数据迁移助手使用 Power BI 的合并的评估报表

本文介绍如何创建用于分析统一的迁移评估的 Power BI 报表。

有关合并的数据迁移助手中创建的迁移评估的信息，请参阅[合并评估报表](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>示例 Power BI 报表

可以从此下载的合并的迁移评估的 Power BI 报表示例[Github 存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)。

以下报表可以包含： 

- [仪表板](#dashboard--details)

  包括快照统计信息和向下钻取报表。

- [在本地升级就绪情况](#on-premises-upgrade-readiness--details)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报表显示您已评估的数据库的百分比升级成功。

- [在本地功能奇偶一致性](#on-premise-feature-parity--details)

  显示目标 SQL Server 版本的功能建议。

- [Azure SQL DB 升级就绪情况](#azure-sql-db-upgrade-readiness--details)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报表显示针对 Azure SQL DB 迁移评估的数据库的百分比升级成功。

- [Azure SQL 数据库不受支持的功能](#azure-sql-db-unsupported-features--details)

  显示了 Azure SQL 数据库 (V12) 中不支持将现有数据库中的功能。

您可以修改这些报表来处理您的环境的更改 Power BI 中的数据源。 

1. 选择向下箭头旁边**编辑查询**，然后选择**数据源设置**。

   ![编辑查询菜单上，数据源设置](../dma/media/DataSourceSettings.png)

1. 选择**更改源...**，然后键入服务器和数据库的值。

   ![更改源、 服务器和数据库](../dma/media/ChangeSource.png)

1. 选择**确定**，然后选择**关闭**。

1. 刷新报表。

   ![刷新 Power BI 报表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>仪表板报表

![仪表板报表](../dma/media/DashboardReport.png)

仪表板会显示有关所有评估的详细信息。 可以使用左侧的切片器要作为筛选依据实例或数据库。 条形图可用于深化到特定的类别，若要查看存在问题的位置。

若要向下钻取，请选择该圆形的条形图的右上角的向下箭头。

![类别向下钻取](../dma/media/CategoryDrillDown.png)

下图中所示设置向下钻取序列 (下**轴**)。 若要更改顺序，请将列拖到所需的顺序。

![可视化效果，条形图坐标轴](../dma/media/VisualizationsAxis.png)

首先按特定的数据库筛选，然后深化到特定类别问题时，此视图将变得更强大的功能。 在以下示例中，例如选择 HR 数据库**SQL01**查看阻止迁移 （重大更改） 的所有对象。

![HR 数据库的重大更改](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>在本地升级准备情况报告

![在本地升级准备情况报告](../dma/media/OnPremisesUpgradeReadinessReport.png)

此报表显示已准备好你的数据库已经迁移到更高版本的 SQL Server 的快照。 此报表中的数据来自 dbo。UpgradeSuccessFactor\_DMAReporting 数据库中的本地视图。

按实例和数据库名称筛选和使用顶部的分数卡，您可以查看哪些可能太迁移数据库的版本。 例如，如果通过 AdventureWorks 2012 数据库进行筛选，可以看到数据库现在可以将移动到报告中列出的所有 SQL Server 版本。 这确定通过确保该数据库和兼容性级别没有重大更改。

![升级成功 AdventureWorks 数据库的因素](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>在本地功能奇偶校验报表

![在本地功能奇偶校验报表](../dma/media/OnPremisesFeatureParityReport.png)

使用此报表突出显示可用于目标 SQL Server 版本中的数据库的新功能。

在漏斗图中选择一项功能，突出显示了在底部的数据，该功能受影响的对象。 在以下示例中，**延伸数据库以节省存储空间**选择功能，并列出表，可以利用此功能。

![Stretch Database 的功能建议](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 升级准备情况报告

![Azure SQL DB 升级准备情况报告](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此报表显示迁移到 Azure SQL 数据库 V12 的数据库准备情况。 此报表中的数据来自 dbo。UpgradeSuccessRanking DMAReporting 数据库中的视图。

### <a name="azure-features-parity-report"></a>Azure 功能奇偶校验报表

![Azure 功能奇偶校验报表](../dma/media/AzureFeaturesParityReport.png)

使用此报表突出显示*实例级别功能*不受 Azure SQL 数据库 V12。

当在漏斗图中选择一项功能时，在底部的数据列出了实例和数据库功能不受支持的。 在以下示例中，选择此功能：**可用性组配置不支持始终在 Azure SQL 数据库中**。  

![Alwayson 可用性组功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL 数据库不受支持的功能报表

![Azure SQL 数据库不受支持的功能报表](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

此报表突出显示了哪些功能不支持为给定**数据库**当目标是 Azure SQL 数据库 (V12)。

通过漏斗图中的数据库名称和功能值筛选，您可以查看详细信息不受支持的功能。 详细信息包括受影响的对象和解决问题的建议。

例如，筛选由 DTC 数据库和**无法升级只读数据库**，可以查看受影响的对象的列表。

![只读数据库不能为升级问题](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另请参阅

[数据迁移助手概述](../dma/dma-overview.md)

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下载](https://powerbi.microsoft.com/)
