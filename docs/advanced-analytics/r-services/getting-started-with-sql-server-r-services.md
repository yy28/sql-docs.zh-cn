---
title: "SQL Server R Services 入门 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 12/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7850d6e302ffa75b368280177ffbe4443fd3378e
ms.lasthandoff: 04/11/2017

---
# <a name="getting-started-with-sql-server-r-services"></a>SQL Server R Services 入门
 构建高级分析解决方案的典型工作流，是从数据浏览和预测性建模开始，而数据科学家开发了被证明可有效满足手头任务的 R 脚本和模型。 准备好脚本和模型后，便可以将它们部署到生产并与现有或新的应用程序集成。   
  
SQL Server R Services 旨在帮助用户完成以下数据科学任务。 可继续使用你最喜欢的 R 或 SQL 工具，但要在无需其他硬件的情况下将分析扩展到数十亿记录、提高性能，并避免不必要的数据移动。 现在，可以将 R 代码放入生产中，而不必用另一种语言重写。 这样，也更易于在使用 SQL 难以实现的统计计算中使用 R。 同时，可以利用 SQL Server 的强大功能，通过使用内存中数据库引擎和列存储索引等功能来实现最佳性能。  
  
以下各部分高度概述了一些典型的分析工作流以及通过 SQL Server R Services 来启用它们的方法。  

> [!TIP]
> 请参阅本教程快速开始。 本教程介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况并安排人员以满足需求。
> 
> [Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r)


  
-   **开发**  
  
     数据科研人员通常使用 R 并借助所选的 R IDE 从其工作站浏览数据和生成预测模型。 数据科研人员可反复进行测试和优化，直到实现良好的预测模型。 
     
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 客户端组件为数据科研人员提供所有必要的工具来展开试验和开发。 这些工具包括 R 运行时、用于提升标准 R 操作性能的 Intel 数学内核库，以及一组支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中执行 R 代码的增强型 R 包。  
  
     数据科研人员可以像平时一样连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后将数据取回到客户端进行本地分析。 但是，更好的解决方案是使用 **ScaleR** API 将计算数据推送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，以避免产生开销较大且不安全的数据移动。  
  
     若要开发 R 解决方案，数据科研人员可以使用支持 R 的、基于 Windows 的任何 IDE，包括 [用于 Visual Studio 的 R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx) 或 RStudio。  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     有关详细信息，请参阅 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  

  
-   **优化**  
  
     在使用 R 分析大型数据集时，数据科研人员通常会遇到性能和伸缩性问题，因为通用运行时实现是单线程的，只能适应可装入本地计算机上可用内存的数据集。 若要获取更好的性能和处理更多的数据，数据科研人员可以使用 **随附的** ScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]API。 **RevoScaleR** 包包含部分最常用 R 函数的实现，这些实现在经过重新设计后可提供并行度和伸缩性。 该包还包含一些函数，可通过将计算数据推送到通常具有大得多的内存和计算能力的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，来进一步提升性能和伸缩性。  
  
     有关详细信息，请参阅 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  
  
-   **部署**  
  
     R 脚本或模型可供生产使用后，数据库开发人员可以在存储过程中嵌入代码或模型，并从应用程序调用保存的代码。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储和运行 R 代码可带来诸多好处：可使用便利的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 接口，并且所有计算将在数据库中发生，从而避免不必要的数据移动。 你可以通过生产环境中的预测模型使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 生成分数，或返回 R 生成的图形并在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]等应用程序中显示这些图形。  
  
     若要进一步优化系统存储过程中嵌入的 R 代码，建议使用可对大型数据集运行的 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) 包 API。 对于多线程、多核心、多进程计算，这些包支持数据库内执行。  
  
     如果你需要将 R 代码部署到生产环境， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可充分体现 R 和 SQL 的优势。 可以使用 R 来实现使用 SQL 时难以实现的统计计算，同时利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的强大优势，借助内存数据库引擎和列存储索引等功能来实现最大性能。  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     有关详细信息，请参阅 [实现 R 代码](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
 
 > [!TIP]
 > 了解有关如何将 SQL Server 与本书中的数据科学集成的详细信息，可从 Microsoft Virtual Academy 免费下载： [Data Science with Microsoft SQL Server 2016](https://mva.microsoft.com/ebooks/)（与 Microsoft SQL Server 2016 集成的数据科学）

-   **管理和监视**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用新的可扩展性体系结构，可保护数据库引擎的安全并隔离 R 会话。 你还可以控制哪些用户可以执行 R 脚本，并可指定 R 代码可以访问哪些数据库。 你可以控制分配给 R 运行时的资源量，以防止海量计算降低服务器的整体性能。  
  
     R 作业在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中运行时，还可以像使用其他存储过程时一样，控制和审核分析人员或者包含 R 脚本的计划作业和创作工作流使用的数据。  
  
     有关详细信息，请参阅 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  
-   **集成**  
  
     你不再需要占用 IT 预算来采购企业工具即可处理某些外部 R 运行时环境。 你可以在熟悉的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]环境中工作，使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]来开发集成的工作流和报告解决方案。  
  
     有关详细信息，请参阅 [在 SQL Server 中创建使用 R 的工作流](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)。  
  
  
## <a name="how-do-i-get-it"></a>如何获取它？  
   
  
+   **安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更高版本，并启用 R Services（数据库中）**  
  
    [设置 SQL Server R Services（数据库中）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
  
-   **设置客户端工作站**  
  
     [设置数据科学客户端](../../advanced-analytics/r-services/set-up-a-data-science-client.md)  
   
> [!TIP]  
> 需要为 R 作业创建一个服务器，但不需要 SQL Server？ 请尝试 [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)。  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>如何使用 SQL Server R Services 运行 R 代码  
 安装完成后，可以通过将 R 嵌入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程中，或者编写使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据的即席 R 脚本在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上运行 R 代码。  
  
-   了解如何从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句调用 R 和在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中返回结果  
  
     [在 Transact-SQL 中使用 R 代码](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   了解使用 SQL Server R Services 创建和部署高级分析解决方案的完整流程  
  
     [数据科学端到端演练](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   了解如何使用 RevoScaleR 包进行可伸缩性和高性能分析，以及如何将 R 计算推送到 SQL Server 计算机  
  
     [对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   将工作中的 R 脚本嵌入到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程中，以便你能够调用用于预测的模型、重新定型模型或从应用程序获取预测  
  
     [适用于 SQL 开发人员的数据库内高级分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 堆栈中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和相关的商业智能工具来自动化机器学习过程。 使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]可以自动化数据准备和报告；使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 Power View 显示 R 图形以及其他报表。  
  
+ 更多示例（包括解决方案模板和示例 R 代码）  
   [SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Microsoft R Server（独立版）入门](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

