---
title: "数据科学深入了解如何： 使用 SQL Server 的 RevoScaleR 包 |Microsoft 文档"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 62bcad211bac049151d5feba79004ba72883196b
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>数据科学深入探讨： RevoScaleR 包使用 SQL Server

本教程演示如何使用增强的 R 包中提供[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]处理 SQL Server 数据并创建可缩放 R 解决方案，通过将服务器用作计算上下文高性能大数据分析。

了解如何创建远程计算上下文，本地和远程计算上下文之间移动数据，并在远程 SQL 服务器上执行 R 代码。 你还了解了如何分析和绘制数据，本地和在远程服务器上，以及如何创建和部署模型。

> [!NOTE]
> 
> 本教程专门使用 SQL Server 数据在 Windows 上，并使用数据库中计算上下文。 如果你想要使用 R 在其他上下文，如 Teradata、 Linux 或 Hadoop，请参阅这些 Microsoft R Server 教程： 
> + [使用 R Server 和 sparklyr](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [Explore R and ScaleR in 25 functions](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)（通过 25 个函数探索 R 和 ScaleR）
> + [要开始使用 Hadoop mapreduce ScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>概述

若要在本教程中遇到了 RevoScaleR 包的灵活性和处理能力你移动数据和交换经常计算上下文。 为了说明，下面是一些的任务在本教程中：

+ 数据最初是从 CSV 文件或 XDF 文件中获取的。 你将数据导入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 RevoScaleR 包中的函数。
+ 使用执行模型的训练和评分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算上下文。 
+ 使用 RevoScaleR 函数来创建新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表以保存你评分的结果。
+ 在服务器上创建两个图形和本地计算上下文。
+ 中的数据模型进行训练[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，在中运行 R[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
+ 提取数据的子集，并将其保存为 XDF 文件，以便在分析中重新使用在本地工作站上。
+ 获取新数据评分，通过打开一个到 ODBC 连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 在本地工作站上完成评分。
+ 创建自定义 R 函数，然后在运行服务器计算上下文执行模拟。

### <a name="article-list-and-time-required"></a>文章列表和所需的时间

本教程需要大约为 75 分钟才能完成，不包括安装程序。

1. [使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [使用 RxSqlServerData 创建 SQL Server 数据对象](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [定义并使用计算上下文](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [创建和运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [实现 SQL Server 数据使用 R 可视化效果](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [创建 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [分数新数据](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [使用 R 转换数据](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [将数据加载到内存中用 rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [创建新的 SQL Server 表使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [使用 rxDataStep 执行区块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [在本地计算上下文中分析数据](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [将数据从 SQL Server 使用 XDF 文件移](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [创建简单模拟](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>目标受众

本教程旨在为数据科学家或已熟悉某种程度上与 R，以及如摘要和模型创建的数据科学任务的人员。  但是，所有的代码提供，因此即使你不熟悉 R，你可以运行的代码和沿用，前提您拥有所需的服务器和客户端环境。

你还应熟悉[!INCLUDE[tsql](../../includes/tsql-md.md)]语法并且知道如何访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库使用这些工具：

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio 中的数据库工具 
+ 免费[mssql 扩展 Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。
  
> [!TIP]
> 在各个课程之间保存 R 工作区，便可轻松地从中断的位置继续。

### <a name="prerequisites"></a>必备条件

- **支持的 R 与 SQL Server**
  
    安装 SQL Server 2016 并使 R Services （数据库）。 或者，安装 SQL Server 2017 和启用机器学习服务并选择 R 语言。
  
-  **数据库权限**
  
    若要运行用于定型模型的查询，必须在存储数据的数据库上具有 **db_datareader** 权限。 若要运行 R，你的用户必须具有的权限，执行任意外部脚本。

-   **数据科学开发计算机**
  
    必须将 RevoScaleR 包和相关的提供程序安装在用作 R 开发环境的计算机上。 若要执行此操作的最简单方法是安装 Microsoft R 客户端，Microsoft R Server （独立） 或机器学习 Server （独立）。 
      
    > [!NOTE] 
    > 不支持其他版本的 Revolution R Enterprise 或 Revolution R Open。
    > 
    > 无法在此教程中，使用 R 的开源分发，因为只有 RevoScaleR 函数可以使用远程计算上下文。
  
-   **其他 R 包**
  
    在本教程中，安装以下程序包： **dplyr**， **ggplot2**， **ggthemes**， **reshape2**，和**e1071**. 本教程提供说明。
  
    必须在两个位置安装所有包： 在用于 R 解决方案开发计算机上并在其中执行 R 脚本的 SQL Server 计算机上。 如果你没有在服务器计算机上安装包的权限，请让管理员。 
    
    **请勿将包安装到用户库。** 必须在 SQL Server 实例使用的 R 包库中安装包。

有关详细信息，请参阅[数据科学演练的先决条件](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

## <a name="next-step"></a>下一步

[使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

