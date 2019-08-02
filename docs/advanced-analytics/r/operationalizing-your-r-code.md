---
title: 使用存储过程的操作 R 代码
description: 在 SQL Server 存储过程中嵌入 R 语言代码, 使其可供任何可以访问 SQL Server 数据库的客户端应用程序使用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: adcac48bc7d90aae5f05a9b671f05e34cc8cf554
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715678"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>在 SQL Server 中使用存储过程的操作 R 代码机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 SQL Server 机器学习服务中的 R 和 Python 功能时, 将解决方案移动到生产环境的最常见方法是在存储过程中嵌入代码。 本文总结了在使用 SQL Server 实现 R 代码时, SQL 开发人员需要考虑的要点。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>使用 T-sql 和存储过程部署生产就绪脚本

传统上, 数据科学解决方案的集成旨在支持性能和集成。 SQL Server 机器学习服务简化了此任务, 因为 R 和 Python 代码可以在 SQL Server 中运行, 并使用存储过程进行调用。 有关在存储过程中嵌入代码的机制的详细信息, 请参阅:

+ [起步SQL Server 中的 "Hello world" R 脚本](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[有关使用存储过程将 R 代码部署到生产中的更全面的示例, 请参阅教程:适用于 SQL 开发人员的 R 数据分析](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>针对 SQl 优化 R 代码的准则

如果事先在 R 或 Python 代码中执行某些优化, 则在 SQL 中转换 R 代码会更容易。 这包括避免导致问题的数据类型、避免不必要的数据转换, 并将 R 代码重写为可轻松参数化的单个函数调用。 有关详细信息，请参阅：

+ [R 库和数据类型](r-libraries-and-data-types.md)
+ [转换 R 代码以在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)
+ [使用 sqlrutils helper 函数](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>将 R 和 Python 与应用程序集成

由于可以从存储过程中运行 R 或 Python, 因此可以从任何可发送 T-sql 语句并处理结果的应用程序中执行脚本。 例如, 您可以通过使用 Integration Services 中的 "[执行 t-sql" 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)或使用可以运行存储过程的另一个作业计划程序, 重新训练某个计划的模型。

评分是一项重要的任务, 可以轻松地自动执行, 也可以从外部应用程序启动。 您可以事先使用 R、Python 或存储过程来训练模型, 并将[模型以二进制格式保存](../tutorials/walkthrough-build-and-save-the-model.md)到表中。 然后, 可以使用以下选项之一, 将该模型作为存储过程调用的一部分加载到变量中:

+ [针对小型批处理优化的实时评分
+ 单行评分, 用于从应用程序调用
+ [本机评分](../sql-native-scoring.md), 适用于不调用 R 的 SQL Server 中的快速批预测

本演练提供了在批处理模式和单行模式下使用存储过程评分的示例:

+ [SQL Server 中 R 的端到端数据科学演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

有关如何在应用程序中集成评分的示例, 请参阅以下解决方案模板:

+ [零售预测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [欺诈检测](https://github.com/Microsoft/r-server-fraud-detection)
+ [客户群集](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提高性能和缩放性

尽管开源 R 语言对大数据集具有已知的限制, 但 SQL Server 机器学习服务附带的[RevoScaleR 包 api](ref-r-revoscaler.md)可以对大型数据集执行操作, 并从多线程、多核、多进程数据库内计算。

如果你的 R 解决方案使用复杂的聚合或涉及大型数据集, 则可以利用 SQL Server 的高效内存中聚合和列存储索引, 然后让 R 代码处理统计计算和评分。

有关如何提高 SQL Server 机器学习中性能的详细信息, 请参阅:

+ [SQL Server R Services 性能优化](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [性能优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>为其他平台或计算上下文改编 R 代码

当你使用 SQL Server 安装程序中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "[独立服务器" 选项](../install/sql-machine-learning-standalone-windows-install.md)或在安装非 SQL 品牌产品时, 针对数据运行的 R 代码可用于其他数据源, 如 Spark over HDFS, Microsoft 机器学习服务器 (以前称为**Microsoft R Server**):

+ [Machine Learning Server 文档](https://docs.microsoft.com/r-server/)

+ [浏览 R 到 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [写入分块算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [在 R 中计算大数据](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [开发自己的并行算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

