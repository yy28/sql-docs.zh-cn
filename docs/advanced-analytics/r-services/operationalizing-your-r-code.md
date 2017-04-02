---
title: "实现 R 代码 | Microsoft Docs"
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
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 实现 R 代码
  数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发者与应用程序开发者、SQL 开发者和数据科学家合作，共同设计解决方案、推荐数据管理方法，并构建和部署解决方案。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为与数据科学家合作的开发者带来了多种优势。  
  
-   **使用 R 脚本与交互 [!INCLUDE[tsql](../../includes/tsql-md.md)]。** 应用程序和数据库开发人员，以及分析师创作报表，可以通过调用系统存储过程从调用的 R 脚本。  
  
     有关基本语法的详细信息，请参阅 [sp_execute_external_script & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 和 [在 T-SQL 中使用 R 代码](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)。  
 
    有关如何实施 R 的扩展示例代码使用存储的过程，请参阅 [SQL 开发人员的数据库中分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)。
  
     与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集成还意味着你可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 执行 R 脚本，并将结果嵌入应用程序中。 例如，你可以创建一个运行 R 脚本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表，然后在报表中同时显示绘图和预测结果。  
  
-   **性能和扩展。** 尽管大家都知道开源 R 语言有限制，RevoScaleR 包 Api 提供的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以对大型数据集进行操作并从中获益多线程、 多核、 多进程在数据库中计算。  
  
     如果你的 R 解决方案使用复杂的聚合或涉及大型数据集，则可以利用 SQL 的高效内存中聚合和列存储索引，然后让 R 代码处理统计计算和评分。  
  
-   **标准的开发和管理工具。** 无需使用其他任何管理或部署工具，所有 R 作业都可通过调用存储过程进行调用。  
  
     此外，你针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据运行的 R 代码，也可针对 Hadoop 等其他数据源运行。  
  
 此部分介绍了要成功转换 R 解决方案并使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]将其部署到生产环境所需了解的概念。  
  
## 本节内容

[使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)

[将 R 代码转换为在 R Services 中使用](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> 相关任务  
  
[性能优化 SQL Server R 服务](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## 另请参阅  
 [SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [sp_execute_external_script & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  