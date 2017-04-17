---
title: "对数据科学的深入探讨：使用 RevoScaleR 包 | Microsoft Docs"
ms.custom: 
ms.date: 09/27/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0c1a21ba4df218920c2bb6cf6fea93bda4d74d66
ms.lasthandoff: 04/11/2017

---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>对数据科学的深入探讨：使用 RevoScaleR 包
本教程将介绍 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中提供的增强版 R 包。 学习如何在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中使用执行 R 包的可扩展企业框架。   数据科学家可使用这些可扩展 R 函数生成可在本地或服务器上下文中运行的自定义 R 解决方案，以支持高性能大数据分析。  
  
本教程将介绍如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 工作站之间移动数据、分析和绘制数据以及创建和部署模型。  
    
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

大约需要一小时完成本教程（不包括安装程序）。  

-   [第 1 课：使用 R 处理 SQL Server 数据](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [第 2 课：创建并运行 R 脚本](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [第 3 课：使用 R 转换数据](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [第 4 课：在本地计算上下文中分析数据](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [第 5 课：创建简单模拟](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### <a name="target-audience"></a>目标受众  
  
本教程专为数据科学家和其他对 R 和数据科学任务（包括浏览、数据分析和模型优化）有一定了解的人设计。  其中已提供了所有代码，因此你可以轻松运行代码并按说明操作，前提是具有所需服务器和客户端环境。  
  
还应熟悉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法，并且知道如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他数据库工具（如 Visual Studio）访问 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 数据库。  
  
> [!TIP]  
> 在各个课程之间保存 R 工作区，便可轻松地从中断的位置继续。  
  
### <a name="prerequisites"></a>先决条件  
  
-   **支持 R 的数据库服务器**  
  
    安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 并启用 SQL Server R 服务（数据库中）。 [SQL Server 2016 联机丛书](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)对此过程进行了说明。  
  
-   **数据库权限**  
  
    若要运行用于定型模型的查询，必须在存储数据的数据库上具有 **db_datareader** 权限。  
  
  
-   **数据科学工作站**  
  
    必须安装 RevoScaleR 包。 执行此操作最简单方法是安装 Microsoft R Server（独立版）或 Microsoft R Client。 有关详细信息，请参阅 [设置数据科学客户端](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)
      
    > [!NOTE] 
    > 不支持其他版本的 Revolution R Enterprise 或 Revolution R Open。 
    > 
    > R 的开放源分布（如 R 3.2.2）在本教程中不起作用，因为只有 ScaleR 函数可使用远程计算上下文。 
  
-   **其他 R 包**  
  
    本教程中，需要安装以下包： **dplyr**、 **ggplot2**、 **ggthemes**、 **reshape2**和 **e1071**。 本教程提供说明。  
  
    还必须在执行定型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装所有包。 请务必将包安装在 SQL Server 使用的 R 包库中。 **请勿将包安装到用户库。** 如果没有在此文件夹中安装包的权限，请让数据库管理员添加包。   
  
有关详细信息，请参阅[数据科学演练的先决条件 (SQL Server R Services)](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)。  
  
## <a name="data-strategies-for-distributed-r-solutions"></a>分布式 R 解决方案的数据策略
    
一般情况下，在本地开发环境中开始编写并运行 R 脚本之前，应花一些时间来规划数据的使用，并确定解决方案的每个部分在何处运行才能实现最佳性能。  

在本教程中，你将体验 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]随附的用于分析数据、构建模块和创建图表的高性能函数。 我们将这些常规函数称为 ScaleR 或 Microsoft R 以区分从其他开放源 R 包派生的函数。 有关 Microsoft R 与开放源 R 的区别的详细信息，请参阅本[入门指南](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products)。 

使用 ScaleR 函数的主要优点在于它们支持使用本地或服务器数据源以及本地或远程计算上下文。  因此，在学习本教程过程中，可考虑为自己的解决方案将要采用的数据策略。
  
-   **要执行何种类型的分析？** 是单独使用，还是与其他人共享模型、结果或图表？
 
    本教程将介绍如何在开发环境和服务器之间来回移动结果以促进共享和分析。 
  
-   **你需要的 R 包支持远程执行吗？** [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 所提供的 ScaleR 包中的所有函数可在远程计算上下文中运行并可使用并行执行。 与此相反，第三方程序包中的函数可能在单线程执行时需要其他资源。 本教程将介绍如何在本地和远程计算上下文之间切换以在需要时利用服务器资源。 还将介绍如何包装 rxExec 中的标准 R 函数以支持远程执行任意 R 函数。
    
  
-   **数据位于何处，它具有什么特征？**  如果数据位于本地，则必须确定是将所有新数据上传到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是在本地定型模型并只将该模型保存到数据库。 但是，部署到生产时，你可能需要从企业数据定型，并使用 ETL 过程清除和加载数据。  
  
-   类似的问题适用于数据计分。 是在工作站上创建用于数据计分的数据管道，还是使用企业数据源？ 数据清理和准备是作为 ETL 过程的一部分执行，还是执行一次性试验？  

    本教程将介绍如何高效并安全地在本地 R 环境和 SQL Server 之间移动数据。 
  
-   **应使用哪个计算上下文？** 建议在本地对示例数据定型模型，然后切换到使用服务器数据进行测试和生产。

    本教程将介绍如何使用 R 在 SQL Server 和 R 之间移动数据、如何使用 XDF 文件处理数据以及如何使用 ScaleR 函数在区块中处理数据。  
  
 
  
## <a name="next-step"></a>下一步  
[第 1 课：使用 R 处理 SQL Server 数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  


