---
title: 机器学习生命周期和团队过程的 SQL Server 机器学习服务
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c06155a433718a068bc914b071f0f738cd236613
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641967"
---
# <a name="machine-learning-lifecycle-and-personas"></a>机器学习生命周期和角色
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

机器学习项目可以很复杂，因为它们需要的技能和一组不同的专业人员的协作。 本指南介绍了机器学习生命周期的数据专业人员参与机器学习和 SQL Server 如何支持需求类型中的主要任务。

> [!TIP]
> 
> 机器学习项目中开始之前，我们建议您查看的工具和所提供的最佳实践[Microsoft Team Data Science Process](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)，或 TDSP。 此过程已通过机器学习整合有关规划和迭代机器学习项目的最佳实践的 microsoft 的顾问。 TDSP 起源于 CRISP-DM，等行业标准，但包含最新的行为，例如 DevOps 和可视化效果。

## <a name="machine-learning-life-cycle"></a>机器学习生命周期

机器学习是一个复杂的过程，涉及的数据在企业中的所有方面和许多机器学习项目最终会运行时间过长而要比预期更复杂。 下面是一些机器学习，需要在企业中的数据专业人员的支持的方法：

+ 机器学习开始使用的目标和业务规则的标识。
+ 机器学习专业人员必须意识到用于存储、 提取和审核数据的策略。
+ 下一步是可能适用的数据的集合。  必须确定数据源，并从传感器和业务应用程序中提取适当的数据。 
+ 机器学习工作的质量是高度依赖于不只是数据不可用，但用于提取、 处理和存储数据的过程的类型。 
+ 任何机器学习项目都不是报告和分析，并可能是客户的参与和反馈的策略不完整。

SQL Server 可帮助许多企业的数据专业人员和机器学习专家之间的间隙桥接：

+ 数据可以存储在本地或云中
+ SQL Server 集成在企业数据处理，其中包括报告和 ETL 的每个阶段
+ SQL Server 支持的数据安全性、 数据冗余和审核
+ 提供了资源调控

## <a name="data-scientists"></a>数据科学家

数据科学家使用各种工具，用于数据分析和机器学习，范围从 Excel 或免费的开源平台到需要深厚的技术知识的昂贵的统计套件。 但是，SQL Server 中使用 R 或 Python 提供了一些独有的优势与这些传统工具相比：

+ 可以开发和测试解决方案通过使用所选的开发环境，然后为 T-SQL 代码的一部分部署 R 或 Python 代码。
+ 将复杂计算关闭数据科研人员的便携式计算机和服务器，从而避免数据移动，以符合企业安全策略上移动。
+ 通过特殊的 R 包和 Api 改进的性能和规模。 不再受 R，单线程、 内存体系结构，并可以处理大型数据集和多线程、 多核、 多进程计算。
+ 代码可移植性：解决方案可以运行在 SQL Server，或在 Hadoop 或 Linux 中使用[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 一次代码，随地部署。

## <a name="application-and-database-developers"></a>应用程序和数据库开发人员

数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发人员可用于应用程序开发人员、 SQL 开发人员和数据科学家设计解决方案、 推荐数据管理方法，并构建或部署解决方案。

与 SQL Server 集成到开发人员提供了许多好处：

+ 数据科学家可在 RStudio 中，而数据开发人员部署使用 SQL Server Management Studio 的解决方案。 没有更多重新编码的 R 或 Python 解决方案。
+ 使用 T-SQL、 R 和 Python 的最佳优化你的解决方案。 可以更加有效地使用。 利用数据库专业人员的知识在比 SQL Server 通过使用内存中列存储索引来提高性能的机器学习解决方案运行复杂的操作，对大型数据集和使用 SQL 基于集的操作的聚合。 
+ 轻松地自动执行任务，必须对大量数据，如生成的预测得分的生产数据重复运行。 
+ 访问参数化 R 或 Python 脚本从任何应用程序使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。 只需调用存储的过程来为模型定型、 生成绘图，或输出的预测。
+ Api 可以流式传输的大型数据集，并从多线程、 多核、 多进程数据库内计算中获益。

有关相关任务的信息，请参阅：
+ [实现 R 代码](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>数据库管理员

数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 

SQL Server 用于必须支持数据科学角色的数据库管理员提供独特的功能：

+ SQL server 的安全性：体系结构[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]可将数据库安全并隔离外部脚本会话执行从数据库实例的操作。 您可以指定谁有权执行机器学习脚本，并使用数据库角色来管理包。

+ 若要确保你的服务器继续照常运行，即使外部脚本遇到问题的单独进程中执行 R 和 Python 的会话。

+ 使用 SQL Server 资源调控允许你控制的内存和分配给外部运行时，以防止海量计算降低服务器的整体性能的过程。

有关相关任务的信息，请参阅：
+ [管理和监视机器学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>架构师和数据工程师

架构师设计集成跨机器学习生命周期的各个方面的工作流。 数据工程师设计并构建 ETL 解决方案并确定如何优化机器学习的特征工程任务。 整体的数据平台必须设计为平衡相互竞争的业务需求。

由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 紧密集成了其他 Microsoft 工具，例如商业智能和数据仓库堆栈、企业云和移动工具、Hadoop 等，因此它可以为想要提升高级分析功能的数据工程师或系统架构师提供一系列好处。

+ 使用系统存储过程填充数据集、 生成图形，或获取预测调用任何 Python 或 R 脚本。 没有多个设计并行工作流中的数据科学和 ETL 工具。 对 Azure 数据工厂和 Azure SQL 数据库的支持，可以容易地使用云机器学习工作流中的数据源。

+ 有关计划和管理机器学习任务，在 SQL Server，基于 Integration Services、 SQL 代理或 Azure 数据工厂中使用标准的自动化工作流。 或者，使用[操作化功能](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)在 Machine Learning Server。

有关相关任务的信息，请参阅：

+ [SQL Server 中创建机器学习工作流](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

