---
title: 操作 R 代码使用存储的过程的 SQL Server 机器学习服务
description: 在 SQL Server 存储过程，以使其可供有权访问 SQL Server 数据库的任何客户端应用程序中嵌入 R 语言代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2d00e96162b492d28f0c0ec107612023c8e15e48
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512594"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>操作 R 代码在 SQL Server 机器学习服务中使用存储的过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用 R 和 Python 功能在 SQL Server 机器学习服务中，将解决方案移至生产环境中最常用的方法时，通过在存储过程中嵌入代码。 本文汇总了 SQL 开发人员来实现使用 SQL Server 的 R 代码时要考虑的关键点。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>部署生产就绪脚本使用 T-SQL 和存储的过程

传统上，数据科学解决方案的集成目的是用于支持性能和集成大量重新编码。 SQL Server 机器学习服务可简化此任务，因为可以在 SQL Server 中运行 R 和 Python 代码，并使用存储的过程调用。 有关存储过程中嵌入代码的技巧的详细信息，请参阅：

+ [快速入门：SQL Server 中的"hello world"R 脚本](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

通过使用存储的过程将 R 代码部署到生产环境的更完整示例，请参阅[教程：SQL 开发人员的 R 数据分析](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>针对 SQl 优化 R 代码的准则

转换 R 代码在 SQL 中的是 R 或 Python 代码中事先完成某些优化，更容易。 其中包括避免会导致问题的数据类型、 避免不必要的数据转换和重写为可以轻松地参数化的单个函数调用的 R 代码。 有关详细信息，请参阅：

+ [R 库和数据类型](r-libraries-and-data-types.md)
+ [转换 R 代码以便在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)
+ [使用 sqlrutils helper 函数](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>与应用程序中集成 R 和 Python

因为你可以从存储过程中运行 R 或 Python，可以从任何应用程序可发送 T-SQL 语句和处理结果来执行脚本。 例如，你可能会重新训练模型按计划通过使用[执行 T-SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)在 Integration Services，或通过使用另一个作业计划程序可以运行存储的过程。

评分是一项重要任务，可以轻松地自动执行，或从外部应用程序启动。 训练模型事先使用 R 或 Python 或存储的过程，并[以二进制格式保存模型](../tutorials/walkthrough-build-and-save-the-model.md)到表。 然后，可以将模型加载到一个变量，作为存储的过程调用，以获得评分从 T-SQL 使用这些选项之一的一部分：

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

开放源代码 R 语言具有已知限制方面大型数据集，虽然[RevoScaleR 包 Api](ref-r-revoscaler.md)附带 SQL Server 机器学习服务可以对大型数据集并从多线程获益多核、 多进程数据库内计算。

如果你的 R 解决方案使用复杂的聚合或涉及大型数据集，可以利用 SQL Server 的高效率的内存中聚合和列存储索引，并让 R 代码处理统计计算和评分。

有关如何改进 SQL Server 机器学习中的性能的详细信息，请参阅：

+ [SQL Server R Services 的性能优化](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [性能优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>调整其他平台的 R 代码或计算上下文

针对运行的同一 R 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用时可对通过 HDFS、 Spark 等其他数据源使用数据[独立服务器选项](../install/sql-machine-learning-standalone-windows-install.md)中 SQL Server 安装程序或者在安装非 SQL 品牌的产品，Microsoft 机器学习服务器 (以前称为**Microsoft R Server**):

+ [机器学习服务器文档](https://docs.microsoft.com/r-server/)

+ [浏览到 RevoScaleR R](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [编写块区的算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [在 R 中的大数据计算](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [开发您自己的并行算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

