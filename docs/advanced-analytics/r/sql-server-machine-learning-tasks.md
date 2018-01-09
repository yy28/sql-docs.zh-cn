---
title: "计算机学习生命周期和团队过程 |Microsoft 文档"
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a39a9061df724175d72e4b38c883fdf2495234ad
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>机器学习生命周期和角色

机器学习项目可能十分复杂，因为它们需要的技能和专业人员一不同组的协作。 本文介绍中的机器学习生命周期的一种数据专业人员参与机器学习和 SQL Server 如何支持需求的主体任务。

> [!TIP]
> 
> 要开始在机器学习项目之前，我们建议你查看的工具和最佳实践提供[Microsoft 团队数据科学过程](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/)，或 TDSP。 此过程是通过机器学习 microsoft 整合规划和迭代机器学习项目的最佳实践的顾问创建的。 TDSP 其根中行业标准，例如简洁-数据挖掘，但包含新的实践，如 DevOps 和可视化效果。

## <a name="machine-learning-life-cycle"></a>计算机学习生命周期

机器学习是一个复杂的过程，该对象涉及在内的数据在企业中，所有方面和许多机器学习项目得到花费的时间长和正在比预期更复杂。 下面是一些机器学习，要求企业中的数据专业人员的支持的方式：

+ 机器学习开头的目标和业务规则的标识。
+ 机器学习专业人员必须要注意的策略存储、 提取和审核数据。
+ 下一步是可能适用的数据的集合。  必须标识数据源，并从传感器和业务应用程序中提取相应的数据。 
+ 机器学习工作的质量是高度依赖于不只是数据不可用，但用于提取、 处理和存储数据的非常进程的类型。 
+ 机器学习项目都是用于报告和分析，以及可能是客户的参与和反馈的策略不完整。

SQL Server 可帮助许多企业数据专业人员和机器学习专家之间的间隙桥接：

+ 数据可以是存储在本地或云中
+ SQL Server 集成的企业数据处理，包括 reporting 和 ETL 每个阶段
+ SQL Server 支持数据安全性、 数据冗余和审核
+ 提供了资源调控

## <a name="data-scientists"></a>数据科学家

数据科学家使用不同的工具，用于数据分析和机器学习，范围从 Excel 或免费的开源平台到需要深厚的技术知识的昂贵的统计套件。 但是，使用 SQL Server R 或 Python 提供了独一无二的好处比较这些传统的工具：

+ 你可以开发和测试解决方案通过使用所选的开发环境，然后 T-SQL 代码的一部分部署 R 或 Python 代码。
+ 移动复杂计算关闭数据科研人员的便携式计算机和服务器上，避免数据移动，以符合企业安全策略上。
+ 通过特殊的 R 包和 Api 改进了性能和可扩展性。 你不再受 R 的单线程、 内存密集型体系结构，并且可以处理大型数据集和多线程、 多核、 多进程计算。
+ 代码可移植性： 在 SQL Server 或 Hadoop 或 Linux，可以运行解决方案使用[机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 一次代码中，部署任何位置。

## <a name="application-and-database-developers"></a>应用程序和数据库开发人员

数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发人员与应用程序开发人员、 SQL 开发人员和数据科学家设计解决方案、 推荐数据管理方法，并设计或部署解决方案。

与 SQL Server 的集成为数据开发人员提供许多好处：

+ 尽管数据开发人员部署使用 SQL Server Management Studio 的解决方案，数据科研人员可在 RStudio、 工作。 没有更多重新编码工作量的 R 或 Python 的解决方案。
+ 使用 T-SQL、 R，和 Python 最佳优化你的解决方案。 可以更有效地使用。 利用数据库专业人员的知识在 SQL 服务器，而不通过使用内存中列存储索引来提高计算机学习解决方案的性能运行对大型数据集的复杂操作和使用 SQL 基于集的操作的聚合。 
+ 轻松自动处理大量数据，例如根据生产数据生成预测评分必须反复运行的任务。 
+ 访问参数化从任何应用程序使用的 R 或 Python 脚本[!INCLUDE[tsql](../../includes/tsql-md.md)]。 只需调用存储的过程来训练模型、 生成绘图，或输出预测。
+ Api 可以流式处理大型数据集和受益于多线程、 多核、 多进程在数据库中计算。

相关任务的信息，请参阅：
+ [实现 R 代码](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>数据库管理员

数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 

SQL Server 为必须支持数据科学角色的数据库管理员提供了唯一的功能：

+ SQL server 的安全： 的体系结构[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使数据库保持安全，并将其隔离的外部脚本的数据库实例的操作的会话执行。 你可以指定谁有权执行机器学习脚本，并使用数据库角色来管理包。

+ 在单独的进程，以确保你的服务器继续按常规方式运行，即使外部脚本遇到问题中执行的 R 和 Python 的会话。

+ 使用 SQL Server 资源调控可让你控制的内存和进程分配给外部运行时，以防止海量计算降低服务器的整体性能。

相关任务的信息，请参阅：
+ [管理和监视机器学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>架构师和数据工程师

架构师设计集成跨计算机学习生命周期的所有方面的工作流。 数据工程师设计并构建 ETL 解决方案确定如何优化功能工程机器学习任务。 整体的数据平台必须用于平衡竞争的业务需求。

由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 紧密集成了其他 Microsoft 工具，例如商业智能和数据仓库堆栈、企业云和移动工具、Hadoop 等，因此它可以为想要提升高级分析功能的数据工程师或系统架构师提供一系列好处。

+ 通过使用系统存储过程来填充数据集、 生成图形，或获取预测调用任何 Python 或 R 脚本。 没有多个设计并行工作流数据科学和 ETL 工具中。 Azure 数据工厂和 Azure SQL Database 支持可以容易地使用机器学习工作流中的云数据源。

+ 有关计划和管理机器学习任务，在 SQL Server，基于 Integration Services、 SQL 代理或 Azure 数据工厂中使用标准的自动化工作流。 或者，使用[操作化功能](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)机器学习 Server 中。

相关任务的信息，请参阅：

+ [在 SQL Server 中创建机器学习工作流](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

