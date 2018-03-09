---
title: "具有可操作性 R 代码 （机器学习服务） |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: c982c62fbe79fffc878465a48ca993b8b720dc41
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="operationalize-r-code-machine-learning-services"></a>具有可操作性 R 代码 （机器学习服务）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据库开发者肩负集成多种技术并将结果整合在一起的任务，以便在整个企业中共享这些结果。 数据库开发人员与应用程序开发人员、 SQL 开发人员和数据科学家设计和部署解决方案。

本文总结了为数据库开发人员实现 R 代码中使用 SQL Server 时要考虑的要点。

## <a name="get-started-with-r-code-in-sql-server"></a>要开始使用 SQL Server 中的 R 代码

传统上，计算机学习解决方案的集成目的是广泛重新编码工作量以支持性能和集成。 但是，移动到生产环境中的 R 和 Python 代码是在 Microsoft 机器学习服务中，要容易得多，因为可以在 SQL Server 中运行代码，并使用调用存储过程。 你可以继续使用熟悉的工具，并且无需安装的 R 开发环境。 

有关基本语法的详细信息，请参阅：

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [在 SQL 中使用 R 代码](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

有关如何你可以将 R 代码部署到生产环境使用存储的过程的示例，请参阅：

+ [数据库中分析的 SQL 开发人员](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="optimize-your-r-code"></a>优化 R 代码

当然，转换 SQL 中 R 代码是更轻松，如果某些优化已事先完成 R 或 Python 代码中。 其中包括避免会导致问题的数据类型、 避免不必要的数据转换，以及重写作为单个函数调用可以轻松地参数化的 R 代码。 有关详细信息，请参阅：

+ [R 库和数据类型](r-libraries-and-data-types.md)

+ [转换在 R Services 中使用的 R 代码](converting-r-code-for-use-in-sql-server.md)

+ [生成 R 使用 sqlrutils 存储过程](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>与应用程序集成 R 和 Python

因为你可以从存储过程来启动机器学习服务，你可以从任何应用程序能够发送 T-SQL 的语句和处理结果执行 R 或 Python 脚本。

例如，通过使用 Integration Services 中的执行 T-SQL 任务或通过另一个作业计划程序可以运行存储的过程可能会重新训练的模型按计划。

评分是一个重要的任务，可以轻松地自动执行，或从外部应用程序启动。 您事先，训练该模型使用 R 或 Python 或存储的过程，并将模型保存到表的二进制格式。 然后，该模型可以加载到一个变量，作为存储的过程调用，使用这些选项之一以从 T-SQL 获得评分的一部分：

+ [实时](../real-time-scoring.md)对于小的批处理评分，优化
+ 单行评分，用于从应用程序的调用
+ [本机评分](../sql-native-scoring.md)，而不会调用 R 从 SQL Server 的快速的批处理预测

本演练提供了评分使用批处理和单行模式中的存储的过程的示例：

+ [端到端 SQL Server 中的数据科学演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

请参阅如何集成应用程序中评分的示例这些解决方案模板：

+ [零售预测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [欺诈行为检测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [群集的客户](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提升性能和可扩展性

尽管已知的开放源代码 R 语言有限制，RevoScaleR 包 Api 可以在大型数据集上运行并从中获益多线程、 多核、 多进程在数据库中计算。

如果 R 解决方案使用复杂的聚合或涉及到大型数据集，你可以利用 SQL Server 的高效率的内存中聚合和列存储索引，并让的 R 代码处理统计计算和评分。

有关如何改进 SQL Server 机器学习中的性能的详细信息，请参阅：

+ [性能优化 SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [性能优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>调整为其他平台的 R 代码或计算上下文

针对运行的同一 R 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据可以对其他数据源，例如 Hadoop，使用和在其他计算上下文。

有关 Microsoft R 所支持的平台的详细信息，请参阅：

+ [Microsoft R 简介](https://docs.microsoft.com/r-server/)

+ [浏览 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

有关如何可以优化你的 Microsoft R 解决方案在大型数据或多个平台上运行的详细信息，请参阅：

+ [编写块区算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [计算在 R 使用大数据](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [开发你自己的并行算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

