---
title: 操作 SQL Server 机器学习服务中的 R 代码 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 41da5cfe2e545bdcbc59f8d557afc599177c9d5e
ms.sourcegitcommit: f083867f97bb740caa211ca37cb046641172b8c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38952460"
---
# <a name="operationalize-r-code-machine-learning-services"></a>操作 R 代码 （机器学习服务）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发人员可用于应用程序开发人员、 SQL 开发人员和数据科学家设计和部署解决方案。

本文汇总了数据库开发人员来实现使用 SQL Server 的 R 代码时要考虑的关键点。

## <a name="get-started-with-r-code-in-sql-server"></a>开始使用 SQL Server 中 R 代码

一直以来，机器学习解决方案的集成目的是用于支持性能和集成大量重新编码。 但是，移动到生产环境中的 R 和 Python 代码是在 SQL Server 机器学习服务，更容易，因为可以在 SQL Server 中运行代码，并使用调用存储过程。 可以继续使用熟悉的工具，并且无需安装 R 开发环境。 

有关基本语法的详细信息，请参阅：

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [在 SQL 中使用 R 代码](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

有关如何您可以将 R 代码部署到生产环境通过使用存储的过程的示例，请参阅：

+ [数据库内分析面向 SQL 开发人员](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="optimize-your-r-code"></a>优化 R 代码

当然，转换 R 代码在 SQL 中的是 R 或 Python 代码中事先完成某些优化，更容易。 其中包括避免会导致问题的数据类型、 避免不必要的数据转换和重写为可以轻松地参数化的单个函数调用的 R 代码。 有关详细信息，请参阅：

+ [R 库和数据类型](r-libraries-and-data-types.md)

+ [转换 R 代码以便在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)

+ [使用 sqlrutils 生成 R 存储过程](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>与应用程序中集成 R 和 Python

因为你可以从存储过程启动机器学习服务，你可以从任何应用程序可发送 T-SQL 语句和处理结果执行 R 或 Python 脚本。

例如，在 Integration Services 中使用执行 T-SQL 任务或使用另一个作业计划程序可以运行存储的过程可能会重新训练模型按计划。

评分是一项重要任务，可以轻松地自动执行，或从外部应用程序启动。 训练模型事先使用 R 或 Python 或存储的过程，并将该模型保存到表的二进制格式。 然后，可以将模型加载到一个变量，作为存储的过程调用，以获得评分从 T-SQL 使用这些选项之一的一部分：

+ [实时](../real-time-scoring.md)针对小批量评分，优化
+ 单行计分，来从应用程序的调用
+ [本机计分](../sql-native-scoring.md)，用于从 SQL Server 而不会调用 R 的快速批预测

本演练提供评分使用批处理和单行模式中的存储的过程的示例：

+ [端到端数据科学演练的 SQL Server 中的 R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

请参阅有关如何将集成的应用程序中评分的示例这些解决方案模板：

+ [零售预测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [欺诈检测](https://github.com/Microsoft/r-server-fraud-detection)
+ [聚类分析的客户](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提高性能和规模

虽然众所周知开放源代码 R 语言存在限制，RevoScaleR 包 Api 可以对大型数据集并从多线程、 多核、 多进程数据库内计算中获益。

如果你的 R 解决方案使用复杂的聚合或涉及大型数据集，可以利用 SQL Server 的高效率的内存中聚合和列存储索引，并让 R 代码处理统计计算和评分。

有关如何改进 SQL Server 机器学习中的性能的详细信息，请参阅：

+ [SQL Server R Services 的性能优化](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [性能优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>调整其他平台的 R 代码或计算上下文

针对运行的同一 R 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据可对其他数据源，例如 Hadoop、 使用和其他计算上下文。

有关 Microsoft R 支持的平台的详细信息，请参阅：

+ [Microsoft R 简介](https://docs.microsoft.com/r-server/)

+ [探索 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

有关如何优化大型数据或多个平台上运行 Microsoft R 解决方案的详细信息，请参阅：

+ [编写块区的算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [在 R 中的大数据计算](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [开发您自己的并行算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

