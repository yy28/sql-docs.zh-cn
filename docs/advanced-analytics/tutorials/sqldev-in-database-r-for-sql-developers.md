---
title: "数据库中 R 分析 SQL 开发人员 （教程） |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e3767912b2b2cd7390b1329ff1c584324e8bd673
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>数据库中 R 分析 SQL 开发人员 （教程）

本教程的目标是 SQL 程序员提供生成机器学习在 SQL Server 中的解决方案的实践经验。 在本教程中，你将学习如何通过 R 代码包装在存储过程中将 R 合并到应用程序或 BI 解决方案。

> [!NOTE]
> 
> 相同的解决方案是在 Python 中可用。 SQL Server 2017 是必需的。 请参阅[数据库中分析面向 Python 开发人员](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概述

构建端到端解决方案的过程通常包括获取并清洗数据、数据探索和功能研发、模型训练和调优，以及最后在生产中部署模型。 开发和测试的实际代码的最佳执行使用专用的开发环境。 ，这可能意味着 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

但是，在创建该解决方案后，可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在本教程中，我们假定您已被授予的解决方案和专注于构建和部署使用 SQL Server 的解决方案所需的所有 R 代码。

- [第 1 课： 下载示例数据](../tutorials/sqldev-download-the-sample-data.md)

    将示例数据集和示例 SQL 脚本文件下载到本地计算机。

- [第 2 课： 将数据导入到 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    执行在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例上创建数据库和表的 PowerShell 脚本，并将示例数据加载到该表。

- [第 3 课： 浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)

    通过从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程调用 R 包和函数来执行基本的数据浏览和可视化。

- [第 4 课： 创建使用 T-SQL 的数据功能](../tutorials/sqldev-create-data-features-using-t-sql.md)

    使用自定义 SQL 函数创建新数据特征。
  
-   [第 5 课： 训练和保存使用 T-SQL 的 R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    生成的存储过程中使用 R 的机器学习模型。 将模型保存到的 SQL Server 表。
  
-   [第 6 课： 实施该模型](../tutorials/sqldev-operationalize-the-model.md)

    将模型保存到数据库后，使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型用于预测。

### <a name="scenario"></a>应用场景

本教程使用的已知的公共数据集，基于在纽约出租车行程。 若要使示例代码更快速地运行，我们创建代表 1%采样的数据。 你将使用此数据来生成预测特定行程是否有可能收到一条提示，或不是，基于例如天、 距离和提取位置的时间的列的二元分类模型。

### <a name="requirements"></a>要求

本教程适用于用户已熟悉基本数据库操作，如创建数据库和表、 将数据导入表，以及创建 SQL 查询。 已提供所有 R 代码，因此不需要任何 R 开发环境。 有经验的 SQL 程序员应该能够通过使用来完成此示例[!INCLUDE[tsql](../../includes/tsql-md.md)]中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，以及通过运行提供的 PowerShell 脚本。

但是，在开始本教程之前, 必须完成下列准备工作：

- 连接到带有 R Services 的 SQL Server 2016 或使用机器学习服务和启用的 R 2017 年 SQL Server 的实例。
- 对于本教程使用的登录名必须有权创建数据库和其他对象，若要上载的数据，选择数据，并运行存储的过程。

> [!NOTE]
> 我们建议你执行**不**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]编写或测试 R 代码。 如果在存储过程中嵌入的代码没有任何问题，则从存储过程返回的信息是通常不足以了解错误的原因。
> 
> 以进行调试，我们建议你使用工具，如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教程中提供的 R 脚本已使用传统的 R 工具进行开发和调试。

## <a name="next-lesson"></a>下一课

[第 1 课： 下载示例数据](../tutorials/sqldev-download-the-sample-data.md)
