---
title: "SQL Server 机器学习任务 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>SQL Server 机器学习任务

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将开源 R 语言的功能和灵活性与企业级工具相结合，用于数据存储和管理、工作流开发，以及报告和可视化。 本主题介绍机器学习生命周期，和 SQL Server 如何支持四个不同的数据专业人员 enagged 机器学习中的需求。

## <a name="machine-learning-life-cycle"></a>机器学习生命周期

机器学习不是短期的任务，而相反的接触的企业中的数据的所有方面的长期的进程。 机器学习开始使用的业务目标和规则、 标识和来自传感器和业务应用程序的数据的集合。 机器学习高度依赖于的提取、 处理和存储数据，过程中，并且在考虑用于存储、 提取和审核数据的策略时越来越重要。 最后，机器学习现在是用于报告和分析，以及客户的参与和反馈策略重要都。



SQL Server 是适合于机器学习的理想选择，因为它可以弥补许多机器学习过程中的空白：

+ 工作方式在本地或云中
+ 集成企业数据处理，包括商业智能的每个阶段
+ 支持改进的数据安全性
+ 提供了资源调控和审核

## <a name="data-professionals-and-how-they-use-machine-learning"></a>数据专业人员和如何它们使用机器学习

### <a name="data-scientists"></a>数据科学家

数据科学家有权访问各种工具数据分析和机器学习，范围从 Excel 或免费的开源平台到需要深厚的技术知识的昂贵的统计套件。 但是，与 SQL Server 的集成提供独特的优势：

+ 通过使用你所选的 R 开发环境开发并测试解决方案。
+ 将计算推送到数据库，在满足企业的安全策略时避免数据移动。
+ 通过特殊的 R 包和 Api 改进了性能和可扩展性。 你不再受 R 的单线程、 内存密集型体系结构，并且可以处理大型数据集和多线程、 多核、 多进程计算。
+ 可以轻松部署到生产环境和企业工具、 应用程序、 其他数据库和仪表板由调用 R 代码。
+ 数据科学家可以部署和更新分析解决方案，同时满足标准要求企业数据管理，包括安全和访问审核
+ 代码可移植性： 轻松地针对 Hadoop 等其他数据源重新使用 R 代码

### <a name="application-and-database-developers"></a>应用程序和数据库开发人员

数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发者与应用程序开发者、SQL 开发者和数据科学家合作，共同设计解决方案、推荐数据管理方法，并构建和部署解决方案。 

与 SQL Server 的集成的数据开发人员可以使用机器学习提供这些优势：

+ 使用熟悉的工具与 R 脚本进行交互。 让数据科学家参与 RStudio，尽管数据开发人员部署使用 SQL Server Management Studio 的解决方案。 没有更多重新编码工作量的 R 或 Python 的解决方案。
+ 通过混合和匹配 SQL 和 R 或 SQL 和 Python 优化。 很多时候，可以更有效地在 T-SQL 中使用 SQL Server 功能，例如内存中 columnstoreindexes 或非常快的聚合运行对大型数据集的复杂操作。 使用机器学习语言有意义，并使用 SQL 来移动或处理数据。
+ 轻松自动处理大量数据，例如根据生产数据生成预测评分必须反复运行的任务。
+ 从使用任何应用程序中执行 R 或 Python 脚本[!INCLUDE[tsql](../../includes/tsql-md.md)]。 只需调用存储的过程来创建参数化的模型、 生成复杂的绘图，或输出预测。
+ **RevoScaleR**和**revoscalepy** Api 可以在大型数据集上运行并从中获益多线程、 多核、 多进程在数据库中计算。

相关任务的信息，请参阅：
+ [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>数据库管理员

数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 

SQL Server 为必须支持数据科学角色的数据库管理员提供了唯一的功能：

+ SQL server 的安全： 的体系结构[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使数据库保持安全，并将其隔离的外部脚本的数据库实例的操作的会话执行。 你可以指定有权执行机器学习脚本的人员以及谁可以安装新的 R 包，使用数据库角色。

+ 在单独的进程，以确保你的服务器继续按常规方式运行，即使外部脚本遇到问题中执行的 R 和 Python 的会话。

+ 使用 SQL Server 资源调控可让你控制的内存和进程分配给外部运行时，以防止海量计算降低服务器的整体性能。

相关任务的信息，请参阅：
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>架构师和 ETL 设计器

架构师设计集成跨计算机学习生命周期的所有方面的工作流。 数据工程师设计和构建 ETL 解决方案以及确定如何优化特征工程任务 tht 是机器学习过程的一部分。 通常情况下，必须将整体的数据平台设计为平衡竞争和补充业务需求。

由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 紧密集成了其他 Microsoft 工具，例如商业智能和数据仓库堆栈、企业云和移动工具、Hadoop 等，因此它可以为想要提升高级分析功能的数据工程师或系统架构师提供一系列好处。

+ 熟悉的开发工具，用于开发 R 和 Python 的解决方案。 可以通过使用系统存储过程来填充数据集、 生成图形，或获取预测调用任何 Python 或 R 脚本。 没有多个设计并行工作流数据科学和 ETL 工具中。 对 Azure 数据工厂和 Azure SQL 数据库的支持，使得易于转换和管理数据，并使用机器学习工作流中的云数据源。

+ 计划和管理在 Microsoft R Server 中使用操作化功能。

相关任务的信息，请参阅：

+ [在 SQL Server 中创建使用 R 的工作流](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)


