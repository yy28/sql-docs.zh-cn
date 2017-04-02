---
title: "适用于 SQL 开发人员的数据库内高级分析（教程） | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 适用于 SQL 开发人员的数据库内高级分析（教程）
本演练旨在向 SQL 程序员介绍使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 生成高级分析解决方案的实践经验。 在本演练中，你将了解如何通过将 R 代码包装在存储过程中从而将 R 合并到应用程序或 BI 解决方案中。  
  
## 概述  
构建端到端解决方案的过程通常包括获取并清洗数据、数据探索和功能研发、模型训练和调优，以及最后在生产中部署模型。 使用针对 R 构建的开发环境，例如 RStudio 或 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 可以以最佳方式执行实际的 R 代码的开发和测试。 但是，在创建该解决方案后，可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
因此，在本演练中，我们假定已向你提供该解决方案所需的所有 R 代码，你将致力于生成和部署已使用 R 进行编码的高级分析解决方案。  
  
-   [步骤 1：下载示例数据](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)。    将示例数据集和示例 SQL 脚本文件下载到本地计算机。  
  
-   [步骤 2：使用 PowerShell 将数据导入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)。  执行在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例上创建数据库和表的 PowerShell 脚本，并将示例数据加载到该表。  
  
-   [步骤 3：浏览和可视化数据](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)。   通过从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程调用 R 包和函数来执行基本的数据浏览和可视化。  
  
-   [步骤 4：使用 T-SQL 创建数据功能](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)。  使用自定义 SQL 函数创建新数据特征。  
  
-   [步骤 5：使用 T-SQL 训练和保存模型](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md)。  使用存储过程生成并保存机器学习模型。  
  
-   [步骤 6：运营模型](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)。  将模型保存到数据库后，使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型用于预测。  
  
> [!NOTE]  
> 我们建议不要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来编写或测试 R 代码。 如果在存储过程中嵌入的 R 代码有任何问题，那么从存储过程返回的信息通常不足以了解错误的原因。   
>   
> 为了进行调试，我们建议使用诸如 RStudio 或 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 之类的工具。 本教程中提供的 R 脚本已使用传统的 R 工具进行开发和调试。  
>   
> 如果你对如何开发可在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中运行的 R 脚本感兴趣，请参阅教程：[数据科学的端到端演练](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)）  
  
### 应用场景  
本演练使用众所周知的 NYC Taxi 数据集。 此公用数据集包含 20 GB 压缩 CSV 文件（未压缩 ~48 GB），描述了 2013 年超过 1.73 亿次个人出租车出行的详细信息，以及每次出行所花费用。 为了使本演练简单而快速，我们创建了一个典型的数据采样：1% 的数据，或 1,703,957 行和 23 列。 在本演练中，使用此数据生成二元分类模型，该模型根据诸如当天的时间、距离和上车地点等列预测特定行程是否可能得到一笔小费。  
  
  
### 要求  
本演练面向已熟悉基本数据库操作的用户，如创建数据库和表、将数据导入表，以及创建 SQL 查询。 已提供所有 R 代码，因此不需要任何 R 开发环境。 有经验的 SQL 编程人员可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或运行提供的 PowerShell 脚本完成本演练。  
  
但是，在开始本演练之前，必须完成以下准备工作：  
  
-   连接到已启用 SQL Server R Services 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例（需要 CTP 3 或更高版本）。 有关详细信息，请参阅安装说明：[安装 SQL Server R Services（数据库内）](https://msdn.microsoft.com/library/mt696069.aspx)  
  
 -   本演练中使用的登录名必须有权创建数据库和其他对象，有权上载数据、选择数据和运行存储过程。  
  
## 下一步  
[步骤 1：下载示例数据](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## 另请参阅  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
