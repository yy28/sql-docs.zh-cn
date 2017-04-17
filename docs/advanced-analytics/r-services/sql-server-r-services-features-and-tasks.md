---
title: "SQL Server R Services 功能和任务 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c88d3baf4a5d25ea92888eedf514126484a4fbb5
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-r-services-features-and-tasks"></a>SQL Server R 服务功能和任务
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将开源 R 语言的功能和灵活性与企业级工具相结合，用于数据存储和管理、工作流开发，以及报告和可视化。 它支持四种不同的数据专业人员和方案的需求。  
  
## <a name="data-scientists-analyze-model-and-score-using-r-and-sql-server"></a>数据科学家：使用 R 和 SQL Server 分析、建模和评分  
 数据科学家有权访问用于数据分析和机器学习的各种工具，包括从熟悉的 Excel 和开源平台到需要深厚的技术知识的昂贵的统计套件。 其中， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 具有独特的优势，因为它允许数据科学家将计算推送到数据库中，避免了数据移动且符合企业的安全策略。 而且，数据科学家创建的 R 代码可以轻松部署到生产环境并由以下熟悉的企业工具和解决方案调用：基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的应用程序、BI 报表工具和仪表板。 数据科学家可使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]部署并更新分析解决方案，同时满足企业数据管理的标准要求，包括安全性，易于部署、管理和监控，以及访问审核。  
  
-   **熟悉的用户界面。**  通过使用你所选的 R 开发环境开发并测试解决方案。  
  
-   **数据库内部处理。**  执行 R 代码并且在托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机上进行计算。 这样无需移动数据。  
  
-   **性能和扩展。**  包含可扩展的 R 语言包和 API，因此你不会再受到 R.语言的单线程、内存受限的架构的限制。你可以处理大型数据集和多线程、多核、多进程计算。  
    
-   **代码的可移植性。**  针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据运行的同一 R 代码可轻松重用于 Hadoop 等其他数据源。  
  
 有关相关任务和概念的详细信息，请参阅[通过 R 进行数据浏览和预测性建模](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  
  
## <a name="application-and-database-developers-deploy-r-solutions"></a>应用程序和数据库开发人员：部署 R 解决方案  
 数据库开发人员负责集成多种技术并将结果整合在一起，以便在整个企业中共享这些结果。 数据库开发人员与应用程序开发人员、SQL 开发人员和数据科学家合作，共同设计解决方案、推荐数据管理方法，并构建和部署解决方案。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为与数据科学家合作的开发人员带来了许多好处。  
  
-   **使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 与 R 脚本进行交互。**  报表开发人员、分析人员和数据库开发人员可以通过调用系统存储过程调用 R 脚本。 如果你的解决方案使用复杂的汇总方法或涉及到大型数据集，则可以在数据库内部执行计算，或者将 R 和 [!INCLUDE[tsql](../../includes/tsql-md.md)]结合使用，具体取决于哪种方法具有最佳性能。 当你需要对大量数据重复运行任务时，例如根据生产数据生成预测评分，与  [!INCLUDE[tsql](../../includes/tsql-md.md)] 的轻松集成是非常受欢迎的。  
  
     与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集成也意味着你可以在使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]的任何应用程序中执行 R 脚本。 例如，可以从 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表轻松调用存储过程，并在报表中生成绘图和预测结果。  
  
-   **性能和扩展。**  虽然众所周知开放源代码的 R 语言存在多种限制，但 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供的 RevoScaleR 包 API 可以对大型数据集执行操作，并从多线程、多核、多进程数据库内计算中获益。  
  
-   **标准的开发和管理工具。**  无需使用其他任何管理或部署工具；所有 R 作业都可通过调用存储过程进行调用。 此外，你针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据运行的 R 代码，也可针对 Hadoop 等其他数据源运行。  
  
 有关相关任务和概念的详细信息，请参阅[实施 R 代码](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
  
## <a name="database-administrators-manage-advanced-analytics-solutions"></a>数据库管理员：管理高级分析解决方案  
 数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为支持数据科学角色的数据库管理员带来了许多好处。  
  
-   **安全性。**  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的体系结构可保证数据库的安全性，并将 R 会话执行从数据库实例操作中隔离出来。  
  
     你可以指定有权执行 R 脚本的人员，并确保使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中定义的相同安全角色来管理 R 作业中使用的数据。  
  
-   **可靠性。**  R 会话是在单独的进程中执行，即使 R 会话遇到问题，也可以确保你的服务器继续照常运行。  
  
-   **资源调控。**  你可以控制分配给 R 运行时的资源量，以防止海量计算降低服务器的整体性能。  
  
 有关相关任务和概念的详细信息，请参阅 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)。  
  
## <a name="architects-and-etl-designers-create-integrated-workflows-that-span-r-and-sql-server"></a>架构师和 ETL 设计人员：创建跨越 R 和 SQL Server 的集成工作流  
 数据工程师设计并构建 ETL 解决方案。 架构师设计数据平台用于满足竞争性业务和补充业务的需求。 由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 紧密集成了其他 Microsoft 工具，例如商业智能和数据仓库堆栈、企业云和移动工具、Hadoop 等，因此它可以为想要提升高级分析功能的数据工程师或系统架构师提供一系列好处。  
  
-   **各种熟悉的开发工具。**  开发 R 解决方案时，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和系统存储过程填充数据集、运行 R 作业，或获取预测数据。 数据科学工具中不再设计并行工作流；请在熟悉的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]环境中生成数据管道。  
  
     需要使用云数据吗？ 对 Azure Data Factory 和 Azure SQL 数据库的支持使其更容易转换和管理数据，并且像使用本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据那样使用工作流中的云数据源。  
  
-   **创建和管理工作流。**  使用系统存储过程计划作业和创建包含 R 脚本的工作流。  
  
 有关相关任务和概念的详细信息，请参阅[在 SQL Server 中创建使用 R 的工作流](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R 服务入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

