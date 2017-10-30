---
title: "对数据科学的深入探讨：使用 RevoScaleR 包 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
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
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51f4a782ad941d8b9a66ba00cbf2b3540478361c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>对数据科学的深入探讨：使用 RevoScaleR 包

本教程演示如何使用增强的 R 包中提供[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]处理 SQL Server 数据并创建可缩放 R 解决方案，通过将服务器用作计算上下文高性能大数据分析。

您将了解如何创建远程计算上下文，本地和远程计算上下文之间移动数据，并在远程 SQL 服务器上执行 R 代码。 你还将了解如何以分析和绘制数据，本地和在远程服务器上，以及如何创建和部署模型。

> [!NOTE]
> 
> 本教程专门使用 SQL Server 数据在 Windows 上，并使用数据库中计算上下文。 如果你想要使用 R 在其他上下文，如 Teradata、 Linux 或 Hadoop，请参阅这些 Microsoft R Server 教程： 
> + [使用 R Server 和 sparklyr](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explore R and ScaleR in 25 functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)（通过 25 个函数探索 R 和 ScaleR）
> + [要开始使用 Hadoop mapreduce ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [获取 RevoScaleR Teradata 启动指南](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>概述

为了说明 ScaleR 包的灵活性和处理能力，需在本教程中频繁移动数据和交换计算上下文。

+ 数据最初是从 CSV 文件或 XDF 文件中获取的。 使用 RevoScaleR 包中的函数将数据导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
+ 将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算上下文中执行模型定型和计分操作。
    使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rx **函数创建新的** 表，保存计分结果。
+ 在服务器上和本地计算上下文中创建图表。
+ 若要定型模型，可使用已存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。 将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上执行所有计算。
+ 提取数据的子集，并在本地工作站上将其保存为 XDF 文件，以便在分析中重复使用。
+ 使用 ODBC 连接从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中提取计分过程中使用的新数据。 在本地工作站上执行所有计算。
+ 最后，使用服务器计算上下文基于自定义 R 函数执行模拟。

### <a name="get-started-now"></a>现在开始操作

本教程需要大约为 75 分钟才能完成，不包括安装程序。

1. [使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [使用 RxSqlServerData 创建 SQL Server 数据对象](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [定义和使用计算上下文](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [创建和运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [实现 SQL Server 数据使用 R 可视化效果](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [创建 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [分数新数据](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [转换数据使用 R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [将数据加载到内存中用 rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [创建新的 SQL Server 表使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [执行使用 rxDataStep 分块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [分析本地计算上下文; 中的数据](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [SQL Server 和 XDF 文件之间移动数据](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [创建简单的模拟](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>目标受众

本教程专为数据科学家和其他对 R 和数据科学任务（包括浏览、数据分析和模型优化）有一定了解的人设计。  但是，所有的代码提供，因此即使你不熟悉 R，您可以轻松地运行的代码和沿用，前提您拥有所需的服务器和客户端环境。

还应熟悉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法，并且知道如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他数据库工具（如 Visual Studio）访问 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 数据库。
  
> [!TIP]
> 在各个课程之间保存 R 工作区，便可轻松地从中断的位置继续。

### <a name="prerequisites"></a>先决条件

- **支持的 R 与 SQL Server**
  
    安装 SQL Server 2016 并使 R Services （数据库）。 或者，安装 SQL Server 2017 和启用机器学习服务并选择 R 语言。 安装过程所述[SQL Server 2016 联机丛书](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)。
  
-  **数据库权限**
  
    若要运行用于定型模型的查询，必须在存储数据的数据库上具有 **db_datareader** 权限。 若要运行 R，你的用户必须具有的权限，执行任意外部脚本。

-   **数据科学开发计算机**
  
    你还必须在 R 开发环境中安装的 RevoScaleR 包和相关的提供程序。 若要执行此操作的最简单方法是安装 Microsoft R 客户端或 Microsoft R Server （独立）。 有关详细信息，请参阅 [设置数据科学客户端](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)
      
    > [!NOTE] 
    > 不支持其他版本的 Revolution R Enterprise 或 Revolution R Open。
    > 
    > R、 R 3.2.2，如的开源分发不会在本教程中，因为只有 RevoScaleR 函数可以使用远程计算上下文。
  
-   **其他 R 包**
  
    本教程中，需要安装以下包： **dplyr**、 **ggplot2**、 **ggthemes**、 **reshape2**和 **e1071**。 本教程提供说明。
  
    所有程序包必须都安装在两个位置： 用于 R 解决方案开发的计算机上和运行 R 脚本的位置的 SQL Server 计算机上。 如果你没有在服务器计算机上安装包的权限，请让管理员。 **请勿将包安装到用户库。** 很重要的包安装在 SQL Server 实例使用的 R 包库。

有关详细信息，请参阅[数据科学演练的先决条件](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。



## <a name="next-step"></a>下一步

[使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


