---
title: 合并评估报表 (SQL Server 数据 Migration Assistant) |Microsoft 文档
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
ms.openlocfilehash: 7192c055b4b9bfb6155f0963c598f9dc4a760c0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>合并评估报表 （数据迁移助手）

命令行可用于执行迁移评估在无人参与模式下，从开始数据迁移助手 2.1 版。 此功能可帮助你大规模运行评估。 中的 JSON 或 CSV 文件形式的评估结果。

可以评估多个数据库中的单个实例化的数据迁移助手的命令行实用工具，还可以将所有的评估结果导出到单个的 JSON 文件。 或者，可以在时间评估一个数据库，稍后将从这些多个的 JSON 文件的结果合并到 SQL 数据库。

有关如何从命令行运行数据迁移助手的信息，请参阅[运行数据迁移助手从命令行](../dma/dma-commandline.md)。 


## <a name="import-assessment-results-into-a-sql-server-database"></a>导入 SQL Server 数据库的评估结果

使用 PowerShell 脚本可在此[Github 存储库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)评估结果从 JSON 文件导入到 SQL Server 数据库。

> [!NOTE]
> PowerShell v5 或更高版本是必需的。

当执行脚本时，你需要提供以下信息： 

- **serverName**: SQL Server 实例名称，你想要导入评估结果 JSON 文件中。

- **databaseName**： 结果获取导入到的数据库名称。

- **jsonDirectory**： 评估结果保存到一个或多个 JSON 文件中的文件夹。

- **processTo**: sql Server

在"执行函数"部分中，添加上述值，如下所示。

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

如果对象尚不存在，PowerShell 脚本在你指定的 SQL 实例中创建以下对象：

- **数据库**– PowerShell 参数中提供的名称

  - 主存储库

- **表**– 报告

  - 用于报告的数据

- **表**-BreakingChangeWeighting

  - 所有的重大更改的引用表。 你可以在此处定义你自己的权重值来影响更准确的百分比 （%） 升级成功排名。

- **视图**– UpgradeSuccessRanking\_OnPrem

  - 视图显示每个数据库，以迁移在本地的成功因素。

- **视图**– UpgradeSuccessRanking\_Azure

  - 视图显示每个数据库，以迁移在本地的成功因素。

- **存储过程**– JSONResults\_插入

  - 用于将数据从 JSON 文件导入 SQL Server。

- **存储过程**– AzureFeatureParityResults\_插入

  - 用于从 JSON 文件的 Azure 功能奇偶校验结果导入到 SQL Server。

- **表类型**– JSONResults

  - 用于保存本地评估的 JSON 结果并将传递给 JSONResults\_插入存储的过程

- **表类型**– AzureFeatureParityResults

  - 用于保存 azure 评估的奇偶校验结果的 Azure 功能，并将传递给 AzureFeatureParityResults\_插入存储的过程

PowerShell 脚本将创建**处理**目录内您提供包含要处理的 JSON 文件的目录。

脚本执行完毕后，结果是导入到表中，报告。

### <a name="viewing-the-results-in-sql-server"></a>在 SQL Server 中查看结果

加载数据后，连接到 SQL Server 实例。 你的屏幕应显示下图中所示：

![SQL Server 数据库中的统一的报表](../dma/media/DMAReportingDatabase.png)

Dbo。报告表包含以其原始形式的 JSON 文件的内容。

## <a name="on-premises-upgrade-success-ranking"></a>在本地升级成功排名

若要查看数据库和其百分比 （%） 成功排位的列表，选择 [dbo]。UpgradeSuccessRanking_OnPrem 视图：

![UpgradeSuccessRaning_OnPrem 视图中的数据](../dma/media/UpgradeSuccessRankingView.png)

在这里看到给定的数据库并什么是不同的兼容级别的升级的成功机会。 因此，例如，HR 数据库所评估针对兼容性级别 100、 110、 120 和 130。 此评估有助于你直观地查看工作量参与迁移到更高版本的 SQL Server 数据库上当前对当前版本。

通常你关注的度量值是多少的重大更改用于给定的数据库。 在前面的示例中，你可以看到 HR 数据库具有兼容性级别 100、 110、 120 和 130 的 50%升级成功因素。

此指标可以受更改 dbo 中的权重值。BreakingChangeWeighting 表。

在下面的示例中，所涉及的修复 HR 数据库中的语法问题工作被认为高因此值为 3 分配给**工作量**。 由于它不会花费长时间才能解决语法问题，因此值为 1 分配给**FixTime**。 由于将有一些成本参与进行更改，因此值为 2 分配给**成本**。 使用此值更改为 2 的混合的 Changerank。

> [!NOTE]
> 评分是范围为 1-5。  1 过低，和 5 较高。 此外，ChangeRank 是计算的列。

![工作量、 FixTime 和成本值语法问题](../dma/media/SyntaxIssueEffort.png)

现在，在此示例查询 dbo 时。UpgradeSuccessRanking_OnPrem 视图中，已删除的重大更改的 HR 数据库升级成功因素。

![HR 数据库的升级成功因素](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 升级成功排名

若要查看的数据库将迁移到 Azure SQL DB 和百分比成功秩列表，选择 [dbo]。UpgradeSuccessRanking_Azure 视图。

![UpgradeSuccessRanking_Azure 视图中的数据](../dma/media/UpgradeSuccessRankingView_Azure.png)

此处你感兴趣的 MigrationBlocker 值。 100.00 意味着将数据库移动到 Azure SQL 数据库 v12 具有 100%成功的排名。

与此视图的区别是，目前不重写用于更改迁移窗口阻止程序规则的权重。

有关使用 Power BI 此数据报告的信息，请参阅[报告使用 PowerBI 你合并评估](../dma/dma-powerbiassesreport.md)。
