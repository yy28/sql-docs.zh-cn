---
title: "SQL Server R 服务功能和任务 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server R 服务功能和任务
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 与数据存储和管理、 工作流开发，并报告和可视化的企业级工具结合的功能和灵活性的开放源代码 R 语言。 它支持四种不同数据专业人员和方案的需求。  
  
## 数据科学家：使用 R 和 SQL Server 分析、建模和评分  
 数据科学家有权访问用于数据分析和机器学习的各种工具，包括从熟悉的 Excel 和开源平台到需要深厚的技术知识的昂贵的统计套件。 其中， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 具有独特的优势，因为它允许数据科学家将计算推送到数据库中，避免了数据移动且符合企业的安全策略。 而且，数据科学家创建的 R 代码可以轻松部署到生产环境并由以下熟悉的企业工具和解决方案调用：基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的应用程序、BI 报表工具和仪表板。 数据科学家可使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]部署并更新分析解决方案，同时满足企业数据管理的标准要求，包括安全性，易于部署、管理和监控，以及访问审核。  
  
-   **熟悉的用户界面。**  通过使用你所选的 R 开发环境开发并测试解决方案。  
  
-   **数据库内部处理。**  执行 R 代码并且在托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机上进行计算。 这样无需移动数据。  
  
-   **性能和扩展。**  包含可缩放的多个 R 包和 Api，因此不再受 R.的单线程、 内存密集型体系结构您可以处理大型数据集和多线程、 多核、 多进程计算。  
    
-   **代码的可移植性。**  针对运行的同一 R 代码 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据可以轻松地重用针对其他数据源，例如 Hadoop。  
  
 相关的任务和概念的详细信息，请参阅 [数据浏览和使用 R 的预测性建模](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  
  
## 应用程序和数据库开发人员：部署 R 解决方案  
 数据库开发人员负责集成多种技术并将结果整合在一起，以便在整个企业中共享这些结果。 数据库开发人员与应用程序开发人员、SQL 开发人员和数据科学家合作，共同设计解决方案、推荐数据管理方法，并构建和部署解决方案。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为与数据科学家合作的开发人员带来了许多好处。  
  
-   **使用 R 脚本与交互 [!INCLUDE[tsql](../../includes/tsql-md.md)]。**  报表开发人员、分析人员和数据库开发人员可以通过调用系统存储过程调用 R 脚本。 如果您的解决方案使用复杂的聚合或涉及到大型数据集，则可以执行在数据库，或使用 R 的混合计算和 [!INCLUDE[tsql](../../includes/tsql-md.md)], ，取决于它提供最佳性能。 当你需要对大量数据重复运行任务时，例如根据生产数据生成预测评分，与  [!INCLUDE[tsql](../../includes/tsql-md.md)] 的轻松集成是非常受欢迎的。  
  
     与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集成也意味着你可以在使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]的任何应用程序中执行 R 脚本。 例如，可以轻松地调用存储的过程从 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表，以调用 R 脚本，并在报表中生成预测以及绘图。  
  
-   **性能和扩展。**  尽管大家都知道开源 R 语言有限制，RevoScaleR 包 Api 提供的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以对大型数据集进行操作并从中获益多线程、 多核、 多进程在数据库中计算。  
  
-   **标准的开发和管理工具。**  无需使用其他任何管理或部署工具；所有 R 作业都可通过调用存储过程进行调用。 此外，你针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据运行的 R 代码，也可针对 Hadoop 等其他数据源运行。  
  
 相关的任务和概念的详细信息，请参阅 [留给 R 代码](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
  
## 数据库管理员：管理高级分析解决方案  
 数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为支持数据科学角色的数据库管理员带来了许多好处。  
  
-   **安全性。**  体系结构 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使数据库保持安全，并将其隔离来自的数据库实例的操作的 R 会话的执行。  
  
     您可以指定谁有权执行 R 脚本，确保在 R 作业中使用的数据托管使用相同的安全角色中定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **可靠性。**  R 会话是在单独的进程中执行，即使 R 会话遇到问题，也可以确保你的服务器继续照常运行。  
  
-   **资源调控。**  你可以控制分配给 R 运行时的资源量，以防止海量计算降低服务器的整体性能。  
  
 有关相关任务和概念的详细信息，请参阅 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)。  
  
## 架构师和 ETL 设计人员：创建跨越 R 和 SQL Server 的集成工作流  
 数据工程师设计并构建 ETL 解决方案。 架构师设计数据平台用于满足竞争性业务和补充业务的需求。 因为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 紧密地集成使用商业智能和数据仓库堆栈、 企业云和移动工具和 Hadoop 等其他 Microsoft 工具，它提供了一系列的好处到想要提升高级的分析数据工程师或系统架构师。  
  
-   **各种熟悉的开发工具。**  开发 R 解决方案时，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和系统存储过程填充数据集、运行 R 作业，或获取预测数据。 数据科学工具中不再设计并行工作流；请在熟悉的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]环境中生成数据管道。  
  
     需要使用云数据吗？ 对 Azure 数据工厂和 Azure SQL Database 的支持使更轻松地转换和管理数据，并且只是工作流中的使用云数据源一样本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
-   **创建和管理工作流。**  计划作业和创作工作流包含 R 脚本，使用系统存储过程。  
  
 相关的任务和概念的详细信息，请参阅 [创建工作流在 SQL Server 中，使用 R](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)。  
  
## 另请参阅  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  