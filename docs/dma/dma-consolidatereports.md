---
title: 导入和合并数据迁移助手评估报表 (SQL Server) |Microsoft Docs
description: 了解如何评估报告从数据迁移助手导入到 SQL Server 数据库，以及如何合并多个报表
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: be9fc224093f0d5ae14372d4674a52589a2d4801
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781768"
---
# <a name="import-and-consolidate-data-migration-assistant-assessment-reports"></a>导入和合并数据迁移助手评估报表

可以使用命令行来执行迁移评估在无人参与模式下，从开始数据迁移助手 2.1 版。 此功能可帮助你大规模运行评估。 在 JSON 或 CSV 文件格式的评估结果。

可以评估多个数据库中的单个实例化的数据迁移助手的命令行实用程序，并将所有评估结果都导出到一个 JSON 文件。 或者，可以在时评估一个数据库和更高版本将这些多个 JSON 文件中的结果合并到 SQL 数据库。

有关如何从命令行运行数据迁移助手的信息，请参阅[运行数据迁移助手从命令行](../dma/dma-commandline.md)。 

## <a name="import-assessment-results-into-a-sql-server-database"></a>导入到 SQL Server 数据库的评估结果

使用此 PowerShell 脚本[Github 存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)的评估结果从 JSON 文件导入到 SQL Server 数据库。

> [!NOTE]
> PowerShell v5 或更高版本是必需的。

在执行脚本时，需要提供以下信息： 

- **serverName**： 你想要导入评估 SQL Server 实例名称会从 JSON 文件。

- **databaseName**： 结果会导入到的数据库名称。

- **jsonDirectory**： 评估结果保存到，在一个或多个 JSON 文件中的文件夹。

- **processTo**: SQLServer

在"执行函数"部分中，添加上述值，如下所示。

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

如果对象已不存在，PowerShell 脚本在指定后，SQL 实例中创建以下对象：

- **数据库**– PowerShell 参数中提供的名称

  - 主存储库

- **表**– 报告

  - 用于报告的数据

- **表**-BreakingChangeWeighting

  - 所有的重大更改的引用表。 此处可以定义自己的权重的值来影响更准确的百分比（%）排名。

- **视图**– UpgradeSuccessRanking\_OnPrem

  - 视图显示每个要在已迁移的本地数据库的成功因素。

- **视图**– UpgradeSuccessRanking\_Azure

  - 视图显示每个要在已迁移的本地数据库的成功因素。

- **存储过程**– JSONResults\_插入

  - 用于从 JSON 文件的数据导入到 SQL Server。

- **存储过程**– AzureFeatureParityResults\_插入

  - 用于 Azure 的功能奇偶校验结果从 JSON 文件导入 SQL Server。

- **表类型**– JSONResults

  - 用于保存在本地评估的 JSON 结果并将传递给 JSONResults\_Insert 存储的过程

- **表类型**– AzureFeatureParityResults

  - 用于保存 azure 评估的奇偶校验结果的 Azure 功能，并将传递给 AzureFeatureParityResults\_Insert 存储的过程

PowerShell 脚本将创建**处理**目录内包含所要处理的 JSON 文件的目录提供。

在脚本完成后，将结果导入到表中，报告。

### <a name="viewing-the-results-in-sql-server"></a>SQL Server 中查看结果

加载数据后，连接到 SQL Server 实例。 屏幕应显示在下图中所示：

![SQL Server 数据库中合并的报告](../dma/media/DMAReportingDatabase.png)

Dbo。报告表包含以其原始格式的 JSON 文件的内容。

## <a name="on-premises-upgrade-success-ranking"></a>在本地升级成功排名

若要查看的数据库和百分比 （%） 成功排名列表，请选择 dbo。UpgradeSuccessRanking_OnPrem 视图：

![UpgradeSuccessRaning_OnPrem 视图中的数据](../dma/media/UpgradeSuccessRankingView.png)

这里您可以看到对于给定的数据库不同的兼容级别的升级的成功几率为何。 因此，例如，HR 数据库已评估对兼容级别 100、 110、 120 和 130。 此评估可以帮助您直观地查看从数据库当前在当前版本迁移到更高版本的 SQL Server 中涉及的工作量。

通常您关心的指标是多少的重大更改适用于给定的数据库。 在上述示例中，可以看到的 HR 数据库都有兼容性级别 100、 110、 120 和 130 的 50%升级成功因素。

此指标可以通过更改 dbo 中的权重值受影响。BreakingChangeWeighting 表。

在以下示例中，修复 HR 数据库中的语法问题所涉及的工作被视为高因此值为 3 分配给**工作量**。 由于它不会花费长时间才能解决语法问题，因此值为 1 分配给**FixTime**。 由于会有一定的费用涉及中进行更改，因此值 2 分配给**成本**。 使用此值更改为 2 的混合的 Changerank。

> [!NOTE]
> 评分是范围为 1-5。  1 为低，而 5 高。 此外，ChangeRank 是计算所得的列。

![工作量、 FixTime 和成本值语法问题](../dma/media/SyntaxIssueEffort.png)

现在，在此示例查询 dbo 时。UpgradeSuccessRanking_OnPrem 视图中，已删除的重大更改的 HR 数据库的升级成功因素。

![HR 数据库升级的成功因素](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 升级成功排名

若要查看的数据库迁移到 Azure SQL DB 和百分比成功排名列表，请选择 dbo。UpgradeSuccessRanking_Azure 视图。

![UpgradeSuccessRanking_Azure 视图中的数据](../dma/media/UpgradeSuccessRankingView_Azure.png)

此处你感兴趣的 MigrationBlocker 值。 100.00 意味着将数据库移动到 Azure SQL 数据库 v12 的 100%成功排名。

此视图的不同之处是，目前不重写更改迁移阻止程序规则的权重。

此数据使用 Power BI 报告的信息，请参阅[报告合并评估使用 PowerBI](../dma/dma-powerbiassesreport.md)。
