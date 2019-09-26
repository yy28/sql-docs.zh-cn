---
title: 使用机器学习模型生成预测和预测
description: 使用 rxPredict 或 sp_rxPredict 实时评分，或预测 T-sql 以了解 SQL Server 机器学习中 R 和 Python 中的预测和预测的本机计分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14ccd4beb2186213cb3d94b10031ac732224f4d9
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271904"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何使用中的机器学习模型生成预测和预测 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用现有模型预测或预测新数据输入的结果是机器学习中的核心任务。 本文枚举 SQL Server 中生成预测的方法。 在这些方法中, 这种方法是高速预测的内部处理方法, 其中速度基于运行时依赖项的增量缩减。 依赖关系越少, 预测越快。

使用内部处理基础结构 (实时评分或本机评分) 附带了库要求。 函数必须来自 Microsoft 库。 CLR 或C++扩展不支持调用开源或第三方函数的 R 或 Python 代码。

下表总结了用于预测和预测的计分框架。 

| 方法           | 接口         | 库要求 | 处理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| 可扩展性框架 | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 无。 模型可以基于任何 R 或 Python 函数 | 数百毫秒。 <br/>在对任何新数据进行评分之前, 加载运行时环境的成本是固定的, 平均三到600毫秒。 |
| [实时评分 CLR 扩展](../real-time-scoring.md) | 序列化模型上的[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | 迅驰RevoScaleR、MicrosoftML <br/>Python: revoscalepy、microsoftml | 平均为数十毫秒。 |
| [本机计分C++扩展](../sql-native-scoring.md) | 预测序列化模型上的[t-sql 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | 迅驰RevoScaleR <br/>Python: revoscalepy | 平均小于20毫秒。 | 

处理的速度和不是输出的实质是一项与众不同的功能。 假设有相同的函数和输入, 评分的输出不应根据所使用的方法而变化。

必须使用支持的函数创建模型, 然后将其序列化为保存到磁盘的原始字节流, 或以二进制格式存储在数据库中。 使用存储过程或 T-sql, 你可以在不使用 R 或 Python 语言运行时的开销的情况下加载和使用二进制模型, 从而在为新输入生成预测评分时加快完成时间。

CLR 和C++扩展的重要性与数据库引擎本身非常接近。 数据库引擎的本地语言是C++, 这意味着在C++运行时用更少的依赖项编写的扩展。 与此相反, CLR 扩展依赖于 .NET Core。 

正如您所料, 平台支持受这些运行时环境的影响。 本地数据库引擎扩展在支持关系数据库的任何位置运行:Windows、Linux、Azure。 具有 .NET Core 要求的 CLR 扩展目前仅适用于 Windows。

## <a name="scoring-overview"></a>评分概述

_评分_是一个两步过程。 首先, 指定已训练的模型以从表中加载。 其次, 将新的输入数据传递给函数, 以生成预测值 (或_评分_)。 输入通常是一种 T-sql 查询, 返回表格或单个行。 您可以选择输出表示概率的单个列值, 也可以将多个值 (如置信区间、错误或其他有用的补充) 输出到预测。

执行一步后, 准备该模型的整个过程, 然后生成分数, 就是这样总结:

1. 使用受支持的算法创建模型。 支持因选择的评分方法而异。
2. 训练模型。
3. 使用特殊的二进制格式序列化模型。
3. 将模型保存到 SQL Server。 通常, 这意味着将序列化模型存储在 SQL Server 的表中。
4. 调用函数或存储过程, 并将模型和数据输入指定为参数。

当输入包含多行数据时, 通常会将预测值作为评分过程的一部分插入到表中。 在从窗体或用户请求获取输入值并将评分返回给客户端应用程序的方案中, 生成单个分数更为典型。 为了在生成连续分数时提高性能, SQL Server 可能会缓存模型, 以便可以将其重新加载到内存中。

## <a name="compare-methods"></a>比较方法

为了保持核心数据库引擎进程的完整性, 对 R 和 Python 的支持在与 RDBMS 处理中的语言处理隔离的双重体系结构中启用。 从 SQL Server 2016 开始, Microsoft 添加了一个扩展性框架, 允许从 T-sql 执行 R 脚本。 SQL Server 2017 中添加了 Python 集成。 

扩展性框架支持在 R 或 Python 中执行的任何操作, 从简单的函数到定型复杂的机器学习模型。 但是, 无论操作的复杂性如何, 双处理体系结构都需要为每个调用调用外部 R 或 Python 进程。 当工作负荷需要从表中加载预先训练的模型, 并在已 SQL Server 的数据中进行评分时, 调用外部进程的开销会增加在某些情况下可能无法接受的延迟。 例如, 欺诈检测需要快速计分才能获得相关。

为了增加欺诈检测等方案的评分速度, SQL Server 将内置计分库添加为C++和 CLR 扩展, 以消除 R 和 Python 启动过程的开销。

[**实时评分**](../real-time-scoring.md)是实现高性能计分的第一个解决方案。 在早期版本的 SQL Server 2017 和更高版本的更新中引入了 SQL Server 2016, 而实时评分依赖于在 RevoScaleR、MicrosoftML (R)、revoscalepy 和microsoftml (Python)。 通过使用**sp_rxPredict**存储过程从任何支持的模型类型生成评分，而无需调用 R 或 Python 运行时。

[**本机计分**](../sql-native-scoring.md)是一项 SQL Server 2017 功能, 可作为本机C++库实现, 但仅适用于 RevoScaleR 和 revoscalepy 模型。 它是最快和更安全的方法, 但支持相对于其他方法的一组较小的函数。

## <a name="choose-a-scoring-method"></a>选择计分方法

平台要求通常规定要使用哪种评分方法。

| 产品版本和平台 | 方法 |
|------------------------------|-------------|
| Windows 上的 SQL Server 2017、SQL Server 2017 Linux 和 Azure SQL 数据库 | T-sql 预测的**本机计分** |
| SQL Server 2017 (仅限 Windows), SQL Server SP1 或更高版本的 2016 R Services | Sp\_rxPredict 存储过程的**实时评分** |

建议通过函数进行本机评分。 使用 sp\_rxPredict 需要启用 SQLCLR 集成。 在启用此选项之前, 请考虑安全问题。

## <a name="serialization-and-storage"></a>序列化和存储

若要将某一模型与任一快速计分选项一起使用, 请使用特殊的序列化格式保存该模型, 该格式已针对大小和评分效率进行了优化。

+ 调用[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) , 将支持的模型写入**raw**格式。
+ 调用[rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)"以重建模型以便在其他 R 代码中使用, 或查看模型。

**使用 SQL**

通过 SQL 代码，你可以使用[sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)来训练模型，并直接将定型模型插入表中的类型为**varbinary （max）** 的列。 有关简单示例, 请参阅[在 R 中创建 preditive 模型](../tutorials/quickstart-r-train-score-model.md)

**使用 R**

在 R 代码中, 从 RevoScaleR 包调用[rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject)函数, 以便将模型直接写入数据库。 **RxWriteObject ()** 函数可从 ODBC 数据源 (如 SQL Server) 中检索 R 对象, 或将对象写入 SQL Server。 API 在简单的键值存储区之后建模。
  
如果使用此函数, 请确保先使用[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)序列化模型。 然后, 将**rxWriteObject**中的*序列化*参数设置为 FALSE, 以避免重复序列化步骤。

将模型序列化为二进制格式很有用, 但如果您使用的是可扩展性框架中的 R 和 Python 运行时环境的评分预测, 则不需要这样做。 可以将原始字节格式的模型保存到文件, 然后从文件读取到 SQL Server。 如果要在环境之间移动或复制模型, 此选项可能会很有用。

## <a name="scoring-in-related-products"></a>相关产品的评分

如果使用的是[独立服务器](r-server-standalone.md)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 则除了存储过程和 t-sql 函数外, 还可以使用其他选项来快速生成预测。 独立服务器和 Machine Learning Server 都支持用于代码部署的*web 服务*的概念。 可以将 R 或 Python 预先训练的模型捆绑为 web 服务, 在运行时调用该模型来评估新的数据输入。 有关详细信息，请参阅以下文章：

+ [什么是 Machine Learning Server 的 web 服务？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什么是操作化？](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [使用 azureml 模型管理-sdk 将 Python 模型部署为 web 服务](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [将 R 代码块或实时模型发布为新的 web 服务](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [适用于 R 的 mrsdeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>请参阅

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [预测 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)