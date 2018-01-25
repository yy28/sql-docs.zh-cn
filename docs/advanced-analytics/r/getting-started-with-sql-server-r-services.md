---
title: "SQL Server 入门机器学习 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 12/07/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: "34"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8a6e15767282d347fc92b7decf2963d85827cf6f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="getting-started-with-sql-server-machine-learning"></a>SQL Server 机器学习入门

SQL Server 中的机器学习服务设计为支持数据科学任务而无需公开你的数据与安全风险或移动数据 unnecesarily。

+ 在 SQL Server 2016 中，您可以使用您最喜爱的 R 工具，但扩展到数十亿个记录分析，同时提高了性能。 机器学习与 SQL Server 集成还意味着无需重新编码即可将 R 代码用于生产。

+ SQL Server 2017 增加 Python 代码中，的支持使用相同的扩展性框架。

本主题介绍使用 R 或 Python（数据库内）的主要方案，并提供资源帮助用户开始使用自己的解决方案。

适用于：SQL Server 2016 R Services、SQL Server 2017 机器学习服务（数据库内）

> [!NOTE]
> SQL Server 2016 仅支持 R 语言。 支持 Python 语言需要 SQL Server 2017 CTP 2.0。

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>步骤 1. 设置 SQL Server 机器学习服务

1. 运行 SQL Server 安装程序并安装至少一个 SQL Server 数据库引擎实例。
2. 添加功能以支持执行外部运行时。
3. SQL Server 2016 会默认添加 R。 在 SQL Server 2017 中，必须选择要添加的语言。 可选择 R 或 Python，也可两者都启用。
4. 完成安装后，执行其他步骤启用外部脚本执行，并重启服务器。

**资源**

+ [设置机器学习与 SQL Server](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> 需要为 R 作业创建一个服务器，但不需要 SQL Server？ 请尝试 [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)。  

## <a name="step-2-develop-your-r-or-python-solutions"></a>步骤 2. 开发 R 或 Python 解决方案

数据科研人员通常在自己的笔记本电脑或开发工作站上使用 R 或 Python 来研究数据并生成和调整预测模型，直到生成效果良好的预测模型。 

使用 SQL Server 中的机器学习服务，用户无需改变这一流程。 安装已完成后，你可以在运行 R 或 Python 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本地或远程：

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **使用您喜欢的 IDE**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 客户端组件为数据科研人员提供所有必要的工具来展开试验和开发。 这些工具包括 R 运行时、用于提升标准 R 操作性能的 Intel 数学内核库，以及一组支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中执行 R 代码的增强型 R 包。  

+ **工作远程或本地**。 数据科研人员可以像平时一样连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后将数据取回到客户端进行本地分析。 但是，更好的解决方案是使用 **ScaleR** API 将计算数据推送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，以避免产生开销较大且不安全的数据移动。

+ **嵌入在 R 或 Python 脚本[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程**。 代码充分优化后，将其封装在一个存储过程中，以避免不必要的数据移动和优化数据处理任务。


**资源**

+ 安装[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)或 RStudio。  

## <a name="step-3-optimize"></a>步骤 3. 优化

当模型准备好根据企业数据进行缩放时，数据科研人员通常会与 DBA 或 SQL 开发人员一起优化以下流程：

+ 特征工程
+ 数据引入和数据转换
+ 计分

通常，使用 R 的数据科研人员在性能和伸缩性两方面都会遇到问题，尤其是在使用大型数据集时。 因为通用运行时实现是单线程的，只能适应可装入本地计算机上可用内存的数据集。 与 SQl Server 机器学习服务集成可以提供多种功能，带来更好的性能，并处理更多的数据：

+ **RevoScaleR**。: 此 R 包中包含的一些最常用 R 函数，重新设计，以提供并行度和缩放实现。 该包还包含一些函数，可通过将计算数据推送到通常具有大得多的内存和计算能力的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，来进一步提升性能和伸缩性。

+ **revoscalepy**。 这个 Python 库是新增的库，仅在 SQL Server 2017 CTP 2.0 中可用。它可以实现 RevoScaleR 中最常用的函数（例如远程计算上下文）和许多支持分布式处理的算法。

+ 选择该任务的最佳语言。  使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的数据操作，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以获得最大性能。 对列进行快速计算时，可使用内存数据库引擎。

**资源**

+ [性能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 和数据优化](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>步骤 4. 部署和使用

R 脚本或模型可供生产使用后，数据库开发人员可以在存储过程中嵌入代码或模型，使保存的 R 或 Python 代码可从应用程序中调用。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储和运行 R 代码可带来诸多好处：可使用便利的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 接口，并且所有计算将在数据库中发生，从而避免不必要的数据移动。

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **安全和可扩展**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用新的可扩展性体系结构，可保护数据库引擎的安全并隔离 R 会话。 你还可以控制哪些用户可以执行 R 脚本，并可指定 R 代码可以访问哪些数据库。 你可以控制分配给 R 运行时的资源量，以防止海量计算降低服务器的整体性能。

+ **计划和审核**。 外部脚本作业中的运行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 可以控制和审核数据由数据科学家。 与计划其他任何 T-SQL 作业和存储过程一样，用户还可以计划作业和创作包含外部 R 或 Python 脚本的工作流。

若要利用 SQL Server 中的资源管理和安全功能，建议在部署过程中执行以下任务：

+ 将 R 代码转换为可以在存储过程中以最佳方式运行的函数
+ 设置安全和锁定特定任务使用的包
+ 启用资源调控

**资源**

+ [R 的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [SQL Server 的 R 包管理](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>快速入门

阅读此演练了解完整的工作流：从研究数据到创建模型，再到将模型部署到 SQL Server。

+ [数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

了解如何使用 RevoScaleR 包实现可伸缩的高性能分析。

+ [对数据科学的深入探讨：使用 RevoScaleR 包](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

特别是对于数据开发人员 - 提供所有 R 代码！ 了解如何在 SQL 存储过程中嵌入 R，以创建或定型模型，并从存储模型中获得预测。

+ [适用于 SQL 开发人员的数据库内高级分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

了解从存储过程中调用 R 的语法。

+ [在 Transact-SQL 中使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>解决方案

有关详细示例，包括行业 = 特定解决方案模板，请参阅[SQL Server 机学习教程](../tutorials/machine-learning-services-tutorials.md)。
