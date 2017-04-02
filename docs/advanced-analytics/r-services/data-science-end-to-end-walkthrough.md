---
title: "数据科学端到端演练 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
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
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 数据科学端到端演练
在此演练中，将使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]开发端到端解决方案以进行预测建模。  
  
此演练基于已知的公共数据集，即纽约市出租车数据集。 你将结合使用 R 代码、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据和自定义 SQL 函数生成一个分类模型，该模型可指示司机在特定出租车行程中获得小费的概率。 你还会将 R 模型部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并使用服务器数据基于该模型生成分数。  
  
此示例可以轻松地扩展到各类现实问题，例如预测客户对销售活动的反应或预测游客在各个活动上的消费。 因为该模型可以从存储过程进行调用，所以你还可以方便地将它嵌入在应用程序中。  
  
**目标受众**  
  
此演练面向 R 开发人员。 你应该已熟悉一些基本数据库操作，如创建数据库、创建表、将数据导入表中以及使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询表。  将向你提供要执行的 SQL 和 R 脚本。  
  
如果你不熟悉 R 但熟悉数据库，本教程会介绍如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]将 R 集成到企业工作流中。 无需进行 R 编码；提供了所有脚本。 你只需要安装某种类型的 R IDE 以运行命令。  
  
**先决条件**  
  
若要完成本教程，你必须可以访问安装了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例。 对于本地环境，准备好可以连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据科学工作站，然后安装所需 R 库。  
  
有关详细信息，请参阅[数据科学演练的先决条件 (SQL Server R Services)](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)。  
  
## <a name="overview"></a>概述  
此演练说明了实现高级分析的典型端到端解决方案。 你需要按顺序完成课程。  
  
||学完本课的估计时间|  
|-|------------------------------|  
|[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />分析过程首先获取用于生成模型的数据。 你将下载一个公共数据集并将它保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中。|30 分钟|  
|[第 2 课：查看和浏览数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />数据科学家通常花费了大量时间来研究数据并准备好数据以便进行建模、创建新特征或根据需要转换数据。  你将使用 SQL 和 R 来浏览数据并生成摘要。|20 分钟|  
|[第 3 课：创建数据功能（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />你将使用 R 中的自定义函数和 [!INCLUDE[tsql](../../includes/tsql-md.md)]创建新数据特征。|10 分钟。|  
|[第 4 课：生成并保存模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />数据准备就绪后，数据科学家会定型和优化模型，评估其性能，并尝试不同参数。 在此演练中，你将创建一个分类模型，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据生成预测。 你还将使用 R 绘制模型的准确性。|15 分钟|  
|[第 5 课：部署和使用模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />最后，你将通过将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库在生产中部署模型，然后从存储过程调用模型以生成预测。|10 分钟。|  
  
## <a name="notes"></a>说明  
由于此演练旨在向 R 开发人员介绍 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此会使用 R 执行尽可能多的操作。这并不意味着 R 一定是适用于每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。 这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。  
  
## <a name="next-step"></a>下一步  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
