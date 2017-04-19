---
title: "在 SQL Server 中创建使用 R 的工作流 | Microsoft Docs"
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
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 212be9df5e05715eb19c55444076367ac6c6663f
ms.lasthandoff: 04/11/2017

---
# <a name="creating-workflows-that-use-r-in-sql-server"></a>在 SQL Server 中创建使用 R 的工作流
  关系数据库是一种高度优化的技术，用于交付进行事务处理、存储和数据查询的可缩放解决方案。 但是，过去，R 解决方案通常依赖于从各种源导入数据（通常为 CSV 格式）来执行进一步的数据浏览和建模。 这种做法不仅低效，而且不安全。  
  
 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以提供多个优势：  
  
-   数据安全性。 R 的强大功能被引入到数据库中，离数据源更近了一步。 避免了浪费性的或不安全的数据移动。  
  
-   速度。 数据库针对基于集的操作进行了优化。 而且，数据库的最新创新（如内存中表和列式数据存储）实现了闪电般的聚合，进一步提升了数据科学。  
  
-   集成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是许多消耗企业资源的其他数据管理任务和应用程序的操作中心点。 使用已在数据库中的数据可以确保数据一致且最新。 你可以依靠包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure 数据工厂的企业数据管道，而非在 R 中处理数据。 可以通过 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 轻松执行结果报告或分析。  
  
 通过恰当地组合 SQL 和 R 来执行不同的数据处理和分析任务，数据科学家和开发人员变得更加高效。 本部分介绍如何将 R 与其他企业解决方案集成，以执行数据转换、分析和报告。  
  
##  <a name="bkmk_ssis"></a> 创建跨 R 和数据库的高效工作流  
 数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于使用 R、Python 或其他语言执行其中许多任务，但对企业数据执行此类工作流时需要与 ETL 工具和过程无缝集成。  
  
 由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持在 R 中通过 Transact-SQL 和存储过程运行复杂的操作，因此，你可以将特定于 R 的任务与现有的 ETL 过程集成，只需执行极少的重新开发工作。 不需要在 R 中执行一连串内存密集型任务，可以使用最有效的工具（包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[tsql](../../includes/tsql-md.md)]）来优化数据准备。  
  
 例如，在以下应用场景中，你可以将 R 与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组合使用：  
  
-   使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务在 SQL 数据库中创建必需的对象  
  
-   使用条件分支切换 R 作业的计算上下文  
  
-   运行生成自己的数据的 R 作业  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用保存在文本变量中的 R 脚本  
  
### <a name="samples-and-resources"></a>示例和资源  
 [Operationalize your machine learning project using SQL Server 2016 SSIS and R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)（使用 SQL Server 2016 SSIS 和 R Services 实施机器学习项目）  
  
 在此博客文章中，你将学习如何执行以下操作：  
  
-   在“执行 SQL 任务”中使用 R 生成数据并将其保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中  
  
-   使用存储过程训练 R 模型并将其存储在数据库中  
  
-   使用“脚本任务”和“执行 SQL 任务”对模型执行评分  
  
##  <a name="bkmk_ssrs"></a> 创建跨 R 和企业报告工具的可视化效果  
 虽然 R 可以创建图表和有趣的可视化效果，但如果没有与外部数据源良好地集成，就意味着必须单独生成每个图表或图形。 共享可能也比较困难。  
  
 借助 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，你可以在 R 中通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程运行复杂的操作，这些操作可通过各种企业报告工具（包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Power BI）轻松处理。  
  
-   使用 直观显示从 R 脚本返回的   
    图形对象 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   在 Power BI 中使用表  
  
## <a name="samples-and-resources"></a>示例和资源  
 [用于 Microsoft Reporting Services (SSRS) 的R Graphics Device](https://rgraphicsdevice.codeplex.com/)  
  
 此 CodePlex 项目提供了代码来帮助你创建自定义报表项，用以将 R 的图形输出呈现为可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表中使用的图像。  通过使用自定义报表，你可以：  
  
-   将使用 R Graphics Device 创建的图表和绘图发布到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仪表板  
  
-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 参数传递到 R 绘图  
  
> [!NOTE]  
>  请注意，支持用于 Reporting Services 的 R Graphics Device 的代码必须安装在 Reporting Services 服务器上以及 Visual Studio 中。 还需要进行手动编译和配置。  
  
  

