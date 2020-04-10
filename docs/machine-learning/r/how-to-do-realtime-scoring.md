---
title: 生成预告和预测
description: 使用 rxPredict 或 sp_rxPredict 进行实时评分，或者使用 PREDICT T-SQL 进行本机评分以在 SQL Server 机器学习中使用 R 和 Python 进行预告和预测。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c07a5b8d3e1b34c0bb33f44a20ab5fff867db922
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117620"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何在 SQL Server 中使用机器学习模型生成预告和预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用现有模型来对新数据输入的结果进行预告和预测是机器学习中的一项核心任务。 本文枚举了在 SQL Server 中生成预测的方法。 这些方法是用于进行高速预测的内部处理方法，预测速度基于运行时依赖项的增量减少。 依赖项越少，预测速度越快。

使用内部处理基础结构（实时评分或本机评分）对库是有要求的。 函数必须来自 Microsoft 库。 CLR 或 C++ 扩展不支持调用开放源代码或第三方函数的 R 或 Python 代码。

下表总结了用于进行预告和预测的评分框架。 

| 方法           | 接口         | 库要求 | 处理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| 可扩展性框架 | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 无。 模型可基于任何 R 或 Python 函数 | 数百毫秒。 <br/>加载运行时环境有一个固定成本，在任何新数据的评分出来之前，平均耗时三百到六百毫秒。 |
| [实时评分 CLR 扩展](../real-time-scoring.md) | 序列化模型上的 [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | R：RevoScaleR、MicrosoftML <br/>Python：revoscalepy、microsoftml | 平均数十毫秒。 |
| [本机评分 C++ 扩展](../sql-native-scoring.md) | 序列化模型上的 [PREDICT T-SQL 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | R：RevoScaleR <br/>Python：revoscalepy | 平均少于 20 毫秒。 | 

处理速度而非输出物质是区分特征。 假设函数和输入相同，已评分的输出不应根据你使用的方法而有所变化。

模型必须是使用受支持的函数创建的，然后被序列化为保存到磁盘或以二进制格式存储在数据库中的原始字节流。 通过使用存储过程或 T-SQL，你可以加载和使用二进制模型，而不会产生 R 或 Python 语言运行时的开销，从而在生成新输入的预测分数时可缩短完成时间。

CLR 和 C++ 扩展的重要性接近于数据库引擎本身。 数据库引擎的本机语言是 C++，这意味着使用 C++ 编写的扩展使用更少的依赖项运行。 与此相反，CLR 扩展依赖于 .NET Core。 

正如你所预期的，平台支持会受到这些运行时环境的影响。 本机数据库引擎扩展在支持关系数据库的任何环境中运行：Windows、Linux、Azure。 具有 .NET Core 要求的 CLR 扩展当前仅适用于 Windows。

## <a name="scoring-overview"></a>评分概述

评分过程分为两个步骤  。 第一步，指定要从表中加载的已定型的模型。 第二步，将新的输入数据传递给函数以生成预测值（或分数）  。 输入通常是一种 T-SQL 查询，会返回表格或各行。 你可以选择输出表示概率的单列值，也可以将多个值（例如置信区间、错误或其他有用的补充）输出到预测中。

退一步看，可以通过以下方式总结准备模型并生成分数的整个过程：

1. 使用受支持的算法创建模型。 支持因你选择的评分方法而有所不同。
2. 定型模型。
3. 使用特殊的二进制格式序列化模型。
3. 将模型保存到 SQL Server。 通常，这意味着将序列化模型存储在 SQL Server 表中。
4. 调用函数或存储过程，从而将模型和数据输入指定为参数。

当输入包含许多行数据时，通常可以更快地将预测值插入到表中，作为评分过程的一部分。 当你获取表单或用户请求中的输入值时，通常会生成一个分数，并且将此分数返回给客户端应用程序。 为了提高生成连续分数时的性能，SQL Server 可能会缓存模型，使它可以被重新加载到内存中。

## <a name="compare-methods"></a>比较方法

为了保持核心数据库引擎进程的完整性，在将语言处理与 RDBMS 处理分隔开来的双体系结构中启用了对 R 和 Python 的支持。 从 SQL Server 2016 起，Microsoft 添加了允许从 T-SQL 执行 R 脚本的扩展性框架。 在 SQL Server 2017 中，添加了 Python 集成。 

扩展性框架支持你可能会在 R 或 Python 中执行的任何操作，从简单的功能到定型复杂的机器学习模型。 但是，双进程体系结构要求在每次调用时都调用一个外部 R 或 Python 进程，无论操作的复杂性如何。 当工作负荷需要从表中加载预定型的模型并根据 SQL Server 中已有的数据对它进行评分时，在某些情况下，调用外部进程的开销会增添无法接受的延迟。 例如，欺诈检测需要能够进行具有针对性的快速评分。

为了提高欺诈检测等方案的评分速度，SQL Server 添加了内置的评分库作为 C++ 和 CLR 扩展，从而消除了 R 和 Python 启动进程的开销。

[实时评分](../real-time-scoring.md)是进行高性能评分的第一个解决方案  。 SQL Server 2017 的早期版本和 SQL Server 2016 的后续更新中引入的实时评分依赖于 CLR 库，这些库代替 R 和 Python 对 RevoScaleR、MicrosoftML (R)、revoscalepy 和 microsoftml (Python) 中 Microsoft 控制的函数进行处理。 使用 sp_rxPredict 存储过程调用 CLR 库以生成任何受支持模型类型的分数，而无需调用 R 或 Python 运行时  。

[本机评分](../sql-native-scoring.md)是一项 SQL Server 2017 功能，已作为本机 C++ 库实现，但仅适用于 RevoScaleR 和 revoscalepy 模型  。 这是速度最快且更加安全的方法，但是相对于其他方法，它支持的功能更少。

## <a name="choose-a-scoring-method"></a>选择评分方法

平台要求通常指示要使用的评分方法。

| 产品版本和平台 | 方法 |
|------------------------------|-------------|
| Windows 版 SQL Server 2017、SQL Server 2017 Linux 和 Azure SQL 数据库 | 使用 T-SQL PREDICT 的本机评分  |
| SQL Server 2017（仅限 Windows）、SP1 或更高版本的 SQL Server 2016 R Services | 使用 sp\_rxPredict 存储过程的实时评分  |

我们建议使用 PREDICT 函数进行本机评分。 使用 sp\_rxPredict 要求启用 SQLCLR 集成。 在启用此选项之前请考虑安全隐患。

## <a name="serialization-and-storage"></a>序列化和存储

若要将模型与任何一个快速评分选项结合使用，请使用特殊序列化格式保存模型，此格式已针对大小和评分效率进行了优化。

+ 调用 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 将受支持的模型写入原始格式  。
+ 调用 [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)` 重构模型以用于其他 R 代码或查看模型。

**使用 SQL**

通过 SQL 代码，你可以使用 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 定型模型，然后将已定型的模型直接插入表中类型为 varbinary(max) 的列中  。 有关简单示例，请参阅[使用 R 创建预测模型](../tutorials/quickstart-r-train-score-model.md)

**使用 R**

在 R 代码中，从 RevoScaleR 包中调用 [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) 函数将模型直接写入数据库。 rxWriteObject() 函数可以从 ODBC 数据源（例如 SQL Server）中检索 R 对象，或将对象写入 SQL Server  。 此 API 是在简单的键值存储后建模的。
  
如果使用此函数，请确保首先使用 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 序列化模型。 然后，将 rxWriteObject 中的 serialize 参数设置为 FALSE，从而避免重复执行序列化步骤   。

虽然将模型序列化为二进制格式是很有用的，但如果要在扩展性框架中使用 R 和 Python 运行时环境对预测进行评分，则不需要这样做。 可以将模型以原始字节格式保存到文件中，然后从此文件中读取到 SQL Server 中。 如果要在环境之间移动或复制模型，此选项则可能有用。

## <a name="scoring-in-related-products"></a>对相关产品进行评分

如果使用的是[独立服务器](r-server-standalone.md)或 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，除了存储过程和 T-SQL 函数外，还有其他选项可用于快速生成预测。 独立服务器和 Machine Learning Server 均支持用于代码部署的 Web 服务概念  。 可以将 R 或 Python 预定型的模型捆绑为 Web 服务，并在运行时调用以评估新数据输入。 有关详细信息，请参阅以下文章：

+ [Machine Learning Server 中的 Web 服务是什么？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什么是操作化？](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [使用 azureml-model-management-sdk 将 Python 模型部署为 Web 服务](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [发布 R 代码块或实时模型作为新的 Web 服务](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [适用于 R 的 mrsdeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>另请参阅

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)