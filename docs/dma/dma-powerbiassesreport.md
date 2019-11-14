---
title: 通过 Power BI 分析合并的评估报告
titleSuffix: Data Migration Assistant
description: 了解如何使用 Power BI 分析在 SQL Server 中导入和合并的数据迁移评估报表
ms.custom: seo-lt-2019
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
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056497"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>使用 Power BI 分析数据迁移助手创建的合并评估报告

本文介绍如何创建 Power BI 报表来分析合并的迁移评估。

有关合并数据迁移助手创建的迁移评估的详细信息，请参阅[合并评估报告](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>示例 Power BI 报表

可以从此[GitHub 存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)下载用于合并迁移评估的 Power BI 报表的示例。

包含以下报表： 

- [板](#dashboard-report)

  包括快照统计信息和向下钻取报表。

- [本地升级准备情况](#on-premises-upgrade-readiness-report)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报告显示评估的数据库的成功升级百分比。

- [本地功能奇偶校验](#on-premises-feature-parity-report)

  显示目标 SQL Server 版本的功能建议。

- [Azure SQL DB 升级准备情况](#azure-sql-db-upgrade-readiness-report)

  数据源是 DMAReporting 数据库中的 UpgradeSuccessRanking 视图。  此报告显示为 Azure SQL DB 迁移评估的数据库的成功升级百分比。

- [Azure SQL DB 不支持的功能](#azure-sql-db-unsupported-features-report)

  显示 Azure SQL 数据库（V12）不支持的现有数据库中的功能。

通过在 Power BI 中更改数据源，可以修改这些报表以使用您的环境。 

1. 选择 "**编辑查询**" 旁边的向下箭头，然后选择 "**数据源设置**"。

   ![编辑查询菜单，数据源设置](../dma/media/DataSourceSettings.png)

1. 选择 "**更改源 ...** "，然后输入服务器和数据库值。

   ![更改源、服务器和数据库](../dma/media/ChangeSource.png)

1. 选择 **"确定"** ，然后选择 "**关闭**"。

1. 刷新报表。

   ![刷新 Power BI 报表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>仪表板报表

![仪表板报表](../dma/media/DashboardReport.png)

该仪表板将显示有关你的所有评估的详细信息。 可以使用左侧的切片器按实例或数据库进行筛选。 您可以使用条形图向下钻取到特定类别，以查看问题所在的位置。

若要向下钻取，请选择条形图右上角有向下箭头的圆圈。

![类别深化](../dma/media/CategoryDrillDown.png)

深化序列的设置如下图所示（在**轴**下）。 若要更改顺序，请将列拖至所需的顺序。

![可视化效果，条形图轴](../dma/media/VisualizationsAxis.png)

当你首次按特定数据库进行筛选，然后向下钻取到特定的类别问题时，此视图将变得更加强大。 在下面的示例中，为实例**sql01-win12**选择了 HR 数据库以查看阻止迁移的所有对象（重大更改）。

![HR 数据库的重大更改](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>本地升级准备情况报表

![本地升级准备情况报表](../dma/media/OnPremisesUpgradeReadinessReport.png)

此报表显示数据库迁移到更高版本的 SQL Server 的准备情况的快照。 此报表中的数据来自 dbo。DMAReporting 数据库中的 UpgradeSuccessFactor\_OnPrem view。

按实例和数据库名称筛选，并使用顶部的 "评分" 卡，可以查看数据库可以迁移的版本。 例如，如果你按 AdventureWorks 2012 数据库进行筛选，则可以看到数据库已准备好移动到报表中列出的所有 SQL Server 版本。 这是通过确保该数据库和兼容性级别没有重大更改而确定的。

![AdventureWorks 数据库的升级成功系数](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>本地功能奇偶校验报表

![本地功能奇偶校验报表](../dma/media/OnPremisesFeatureParityReport.png)

使用此报表突出显示可用于目标 SQL Server 版本中的数据库的新功能。

在漏斗图中选择一项功能时，底部的数据将突出显示该功能影响的对象。 在下面的示例中，选择了**用于存储空间节约功能的 Stretch database** ，并列出了可从此功能获益的表。

![Stretch Database 功能建议](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 升级准备情况报表

![Azure SQL DB 升级准备情况报表](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此报告显示要迁移到 Azure SQL 数据库 V12 的数据库就绪情况。 此报表中的数据来自 dbo。DMAReporting 数据库中的 UpgradeSuccessRanking 视图。

### <a name="azure-features-parity-report"></a>Azure 功能奇偶校验报表

![Azure 功能奇偶校验报表](../dma/media/AzureFeaturesParityReport.png)

使用此报告突出显示 Azure SQL 数据库 V12 不支持的*实例级功能*。

当您在漏斗图中选择某个功能时，底部的数据将列出不支持的实例和数据库功能。 在以下示例中，已选择此功能： **AZURE SQL 数据库中不支持 Always On 可用性组配置**。  

![Always on 可用性组功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 不支持的功能报表

![Azure SQL DB 不支持的功能报表](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

此报告突出显示了在目标为 Azure SQL Database （V12）的情况下给定**数据库**不支持的功能。

通过按漏斗图中的数据库名称和功能值进行筛选，可以查看有关不受支持的功能的详细信息。 详细信息包括哪个对象受到影响，以及解决问题的建议。

例如，无法升级 DTC 数据库和**只读数据库**的筛选，您可以看到受影响的对象的列表。

![无法升级只读数据库问题](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另请参阅

[数据迁移助手概述](../dma/dma-overview.md)

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下载](https://powerbi.microsoft.com/)
