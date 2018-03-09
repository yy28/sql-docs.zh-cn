---
title: "R 和 SQL Server 的端到端数据科学演练 |Microsoft 文档"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: eee99c95b17438fa810501b653a83538e658b205
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R 和 SQL Server 的端到端数据科学演练
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本演练中，你将开发基于 Microsoft R 与 SQL Server 2016 或 SQL Server 自 2017 年的预测性建模的端到端解决方案。

此演练基于常用的公共数据集，即纽约市出租车数据集。 你使用的 R 代码组合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据和自定义 SQL 函数来生成分类模型，该值指示该驱动程序可能会收到一个特定 taxi 行程的提示的概率。 你还可以部署到你 R 模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并使用服务器数据来生成基于模型的分数。

此示例可以扩展到所有类型的现实问题，例如预测销售活动的客户响应或预测支出或事件的参与情况。 由于该模型可以调用存储过程中，您可轻松地将它嵌入应用程序。

由于本演练旨在引入 R 开发人员[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，只要有可能使用 R。 但是，这并不意味着 R 一定是每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。  这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。 我们尝试指出的是可能的优化此过程。

> [!NOTE]
> 本演练最初是针对 SQL Server 2016 进行开发和测试的。 但是，屏幕快照和过程已更新为使用最新版本的 SQL Server Management Studio，可与 SQL Server 2017 配合工作。

## <a name="overview"></a>概述

估计时间不包括安装程序。 有关详细信息，请参阅[演练先决条件](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

|主题列表|估计时间|
|-|------------------------------|
|[准备 R 演练数据](../tutorials/walkthrough-prepare-the-data.md) <br /><br />获取用于生成模型的数据。 下载一个公共数据集并将其加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中。|30 分钟|
|[使用 SQL 探索数据](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />了解使用 SQL 工具和摘要数据。|10 分钟。|
|[使用 R 汇总数据](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />使用 R 来浏览数据并生成摘要。|10 分钟。|
|[创建在 SQL Server 中使用 R 的图形](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />通过混合使用 R 和 SQL 在本地和远程计算上下文中创建绘图。|10 分钟。|
|[创建使用 R 和 T-SQL 数据功能）](../tutorials/walkthrough-create-data-features.md) <br /><br />在 R 和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用自定义函数执行特征工程。 针对特征化任务，比较 R 和 T-SQL 的性能。 |10 分钟。|
|[生成 R 模型并将其保存在 SQL Server](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />训练和优化预测模型。 评估模型性能。 本演练创建分类模型。 使用 R 绘制模型的准确性。|15 分钟|
|[部署使用 SQL Server 的 R 模型](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />通过将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库在生产环境中部署模型。 从存储过程调用模型以生成预测结果。|10 分钟。|

### <a name="intended-audience"></a>目标的受众

此演练面向 R 或 SQL 开发人员。 它提供了如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将 R 集成到企业工作流的简介。  你应熟悉数据库操作，如创建数据库和表、 导入数据，并运行查询。

+ 将包含所有 SQL 和 R 脚本。
+ 你可能需要修改脚本，在你的环境中运行中的字符串。 你可以使用任何代码编辑器，如[Visual Studio Code](https://code.visualstudio.com/Download)。

### <a name="prerequisites"></a>必要條件

+ 你必须有权的 SQL Server 2016 实例或 SQL Server 自 2017 年的评估版。
+ 在 SQL Server 计算机上必须至少有一个实例已安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。
+ 如果你想要从远程计算机，例如便携式计算机或其他联网的计算机中运行 R 命令，则必须安装 Microsoft R Open 的库。 你可以安装 Microsoft R 客户端或 Microsoft R Server。 远程计算机必须能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
+ 如果你需要将客户端和服务器放在同一台计算机上，请务必安装一组单独的 Microsoft R 库中从"远程"的客户端发送 R 脚本。 不要使用安装的 R 库用于 SQL Server 实例为此目的。

有关如何设置这些服务器和客户端环境的详细信息，请参阅[R 和 SQL Server 数据科学演练先决条件](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

## <a name="next-lesson"></a>下一课

[准备 R 演练数据](../tutorials/walkthrough-prepare-the-data.md)
