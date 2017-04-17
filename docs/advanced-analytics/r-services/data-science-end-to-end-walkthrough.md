---
title: "数据科学端到端演练 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4806090392cb84ec9bf333021bc6f53e008575e2
ms.lasthandoff: 04/11/2017

---
# <a name="data-science-end-to-end-walkthrough"></a>数据科学端到端演练
在此演练中，将使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]开发端到端解决方案以进行预测建模。  
  
此演练基于常用的公共数据集，即纽约市出租车数据集。 你将结合使用 R 代码、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据和自定义 SQL 函数生成一个分类模型，该模型可指示司机在特定出租车行程中获得小费的概率。 你还会将 R 模型部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并使用服务器数据基于该模型生成分数。  
  
此示例可以轻松地扩展到各类现实问题，例如预测客户对销售活动的反应或预测游客在各个活动上的消费。 因为该模型可以从存储过程进行调用，所以你还可以方便地将它嵌入在应用程序中。  
  
**目标受众**  
  
此演练面向 R 或 SQL 开发人员。 它提供了如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将 R 集成到企业工作流的简介。  你应该已熟悉一些数据库操作，如使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 创建数据库和表、导入数据以及创建查询。  

+ 将向你提供要执行的 SQL 和 R 脚本。  
+ 无需进行 R 编码；提供了所有脚本。 
  
**先决条件**  
  
+ 必须可以访问 SQL Server 2016 实例或 SQL Server vNext 评估版。 
+ 在 SQL Server 计算机上必须至少有一个实例已安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 
+ 若要运行 R 命令，需要安装有 R IDE 和 Microsoft R Open 库的单独计算机。 它可以是笔记本电脑或其他联网计算机，但它必须能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
有关如何设置这些服务器和客户端环境的详细信息，请参阅[数据科学演练的先决条件 (SQL Server R Services)](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)。  
  
## <a name="what-the-walkthrough-covers"></a>本演练所包含的内容  

请注意，估计时间不包括安装。
  
|课程列表|估计时间|  
|-|------------------------------|  
|[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />获取用于生成模型的数据。 下载一个公共数据集并将其加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中。|30 分钟|  
|[第 2 课：查看和浏览数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />浏览数据、为建模准备数据，并创建新的功能。  你将使用 SQL 和 R 来浏览数据并生成摘要。|20 分钟|  
|[第 3 课：创建数据功能（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />在 R 和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用自定义函数执行特征工程。 针对特征化任务，比较 R 和 T-SQL 的性能。 |10 分钟。|  
|[第 4 课：生成并保存模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />训练和优化预测模型。 评估模型性能。 本演练创建分类模型。 使用 R 绘制模型的准确性。|15 分钟|  
|[第 5 课：部署和使用模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />通过将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库在生产环境中部署模型。 从存储过程调用模型以生成预测结果。|10 分钟。|  
  
### <a name="notes"></a>说明

+ 本演练旨在向 R 开发人员介绍 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此尽可能使用 R。 这并不意味着 R 一定是每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。  这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。 我们会在此过程中指出可能的优化。 
+ 本演练最初是针对 SQL Server 2016 进行开发和测试的。 但是，屏幕截图和过程已更新以使用 SQL Server Management Studio（适用于 SQL Server vNext）的最新版本。
  
## <a name="next-step"></a>下一步  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  


