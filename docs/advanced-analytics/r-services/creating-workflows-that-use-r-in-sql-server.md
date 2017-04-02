---
title: "在 SQL Server 中创建使用 R 的工作流 | Microsoft Docs"
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
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 在 SQL Server 中创建使用 R 的工作流
  关系数据库是一项高度优化的事务处理、 存储和查询数据的交付可扩展解决方案技术。 但是，以前 R 解决方案具有通常依赖于从各种源，通常以 CSV 格式，以执行进一步的数据浏览和建模导入数据。 这种做法不仅低效，而且不安全。  
  
 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供多个优点︰  
  
-   数据安全性。 R 的强大功能引入到数据库中，更接近于数据源。 避免了浪费或不安全的数据移动。  
  
-   速度快。 数据库最适于基于集的操作。 此外，在数据库中的最新创新如内存中表和列式数据存储的其他数据科学通过提高既快速的聚合。  
  
-   集成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是用于许多其他数据管理任务和使用企业应用程序的操作的中心点。 使用数据库中已有的数据可确保数据是一致和最新。 而不是在 R 中处理数据，您可以依赖于企业数据管道，其中包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure 数据工厂。 报告的结果或分析很容易通过 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
 通过恰当地组合 SQL 和 R 来执行不同的数据处理和分析任务，数据科学家和开发人员变得更加高效。 本部分介绍如何将 R 与其他企业解决方案集成，以执行数据转换、分析和报告。  
  
##  <a name="bkmk_ssis"></a> 创建跨 R 和数据库的高效工作流  
 数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于执行很多这些任务中 R、 Python 或另一种语言;但是，企业的数据执行这样的工作流需要与 ETL 工具和过程无缝集成。  
  
 因为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使您能够通过 TRANSACT-SQL 和存储的过程，在 R 中运行复杂的操作将与现有的 ETL 过程，而无需最小重新开发工作中集成 R 特定的任务。 而不是在 R 中执行的内存 ntensive 任务链，数据准备可使用优化的最有效的工具，其中包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 例如，可以合并与 R [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在这种情况下︰  
  
-   使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务以在 SQL database 中创建必需的对象  
  
-   使用条件分支切换 R 作业的计算上下文  
  
-   运行生成自己的数据的 R 作业  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用保存在文本变量中的 R 脚本  
  
### 示例和资源  
 [使您使用 SQL Server 2016 SSIS 和 R 服务的机器学习项目](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 在这篇博客文章，您将学习如何︰  
  
-   在执行 SQL 任务中使用 R 生成数据并将保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   可以为 R 模型定型并将其存储在数据库中使用存储的过程  
  
-   执行上使用脚本任务和执行 SQL 任务的模型评分  
  
##  <a name="bkmk_ssrs"></a> 创建跨 R 和企业报告工具的可视化效果  
 虽然 R 可以创建图表和有趣的可视化效果，但如果没有与外部数据源良好地集成，就意味着必须单独生成每个图表或图形。 共享也很难。  
  
 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，您可以在 R 中通过运行复杂的操作 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程、 轻松地可供企业报告工具，其中包括各种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Power BI。  
  
-   直观显示从 R 脚本返回的图形对象   
    使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   使用 Power BI 中的表  
  
## 示例和资源  
 [用于 Microsoft Reporting Services (SSRS) 的 R 图形设备](https://rgraphicsdevice.codeplex.com/)  
  
 本 CodePlex 项目提供了代码以帮助您创建自定义报表项呈现为图像，可在 R 的图形输出 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表。  通过使用自定义报表项，您可以︰  
  
-   将图表和图形创建使用 R 图形设备连接到发布 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仪表板  
  
-   传递 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 参数 R 图形  
  
> [!NOTE]  
>  请注意，在 Reporting Services 服务器上，以及在 Visual Studio 中，必须将安装为 Reporting Services 支持 R 图形设备的代码。 手动编译和配置也是必需的。  
  
  