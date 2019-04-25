---
title: 生成预测和使用机器学习模型的 SQL Server 机器学习服务的预测
description: 使用 rxPredict 或 sp_rxPredict 用于本机的预测评分和预测 R 和 SQL Server 机器学习中的 Pythin 中实时评分或预测的 T-SQL。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 001b90eafd26c90f730e5647f0dc62d756ca9d1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503772"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何生成预测和使用 SQL Server 中机器学习模型的预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用现有的模型来预测或预测新数据输入的结果是机器学习中的核心任务。 这篇文章枚举用于在 SQL Server 中生成预测的方法。 内部处理方法对于高速预测，速度基于增量降低方法在运行时依赖项。 较少依赖项意味着更快的预测。

使用内部处理基础结构 （实时或本机评分） 附带了库要求。 函数必须是从 Microsoft 库。 在 CLR 中不支持调用的开源或第三方函数的 R 或 Python 代码或C++扩展。

下表总结了用于预测和预测的评分框架。 

| 方法           | 接口         | 库要求 | 处理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| 可扩展性框架 | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 无。 模型可以基于任何 R 或 Python 函数 | 数百毫秒。 <br/>加载运行时环境都有固定的成本，求平均值三到六个 100 毫秒之前的任何新数据进行评分。 |
| [实时评分的 CLR 扩展](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)上序列化模型 | :RevoScaleR, MicrosoftML <br/>Python: revoscalepy microsoftml | 数十毫秒，平均。 |
| [本机计分C++扩展](../sql-native-scoring.md) | [预测 T-SQL 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)上序列化模型 | :RevoScaleR <br/>Python: revoscalepy | 平均小于 20 毫秒。 | 

加快处理速度并不输出的实质是区别性功能。 假设使用的相同的功能和输入，经过评分的输出应不因你使用的方法。

必须使用受支持的函数，创建的模型，然后将其序列化为原始字节流保存到磁盘，或存储在数据库中的二进制格式。 使用 T-SQL 或存储的过程，可以加载并使用二进制模型无需使用的 R 或 Python 语言运行时间，从而更快的速度完成生成预测得分的新输入时。

CLR 的重要性和C++扩展插件是到数据库引擎本身的邻近性。 数据库引擎的本地语言是C++，这意味着编写扩展插件C++运行较少依赖项。 与此相反，CLR 扩展依赖于.NET Core。 

正如您所料，会在这些运行的时环境中受平台支持。 本机数据库引擎扩展任意关系数据库支持位置运行：Windows，Linux，Azure。 使用.NET Core 要求的 CLR 扩展目前仅 Windows。

## <a name="scoring-overview"></a>评分概述

_评分_是一个两步过程。 首先，指定要从表加载的已训练的模型。 第二个，传递新输入到函数，以生成预测值的数据 (或_分数_)。 输入通常是返回表格或单个行的 T-SQL 查询。 可以选择可输出单个列的值表示概率，也可能会输出多个值，如置信区间、 错误或预测其他有用的补充。

一步后退、 准备模型的整个过程，然后生成评分可总结这种方式：

1. 创建使用受支持的算法的模型。 支持因你选择的评分方法而异。
2. 训练该模型。
3. 序列化在模型中使用特殊的二进制格式。
3. 将模型保存到 SQL Server。 通常这意味着在 SQL Server 表中存储的序列化的模型。
4. 调用的函数或存储的过程，作为参数指定的模型和数据输入。

如果输入包含很多行数据，它通常是更快地将预测值插入表中评分过程的一部分。 生成单个评分是更典型的场景，从窗体或用户请求，获取输入的值并返回到客户端应用程序的分数中。 为了提高性能，当生成连续的分数时，SQL Server 可能会缓存模型，以便可以重新加载到内存。

## <a name="compare-methods"></a>比较方法

若要保留核心数据库引擎进程的完整性，请在双体系结构中隔离从 RDBMS 处理语言处理的启用对 R 和 Python 的支持。 从 SQL Server 2016 开始，Microsoft 增加了一种可扩展性框架，允许在 T-SQL 中执行 R 脚本。 在 SQL Server 2017 中，添加了 Python 集成。 

可扩展性框架支持可能会在 R 或 Python，到训练复杂机器学习模型的简单函数范围中执行任何操作。 但是，双进程体系结构需要调用外部 R 或 Python 进程为每个调用，而不考虑操作的复杂性。 工作负荷需要从表中加载预先训练的模型和数据已在 SQL Server 上对其评分，调用外部进程的开销会添加可在某些情况下不可接受的延迟。 例如，欺诈检测需要快速的评分相关。

若要增加评分的速度，如欺诈检测方案进行，SQL Server，添加了内置评分库作为C++和 CLR 扩展，消除了 R 和 Python 启动进程的开销。

[**实时评分**](../real-time-scoring.md)是高性能评分的第一个解决方案。 在早期版本的 SQL Server 2017 和更高版本更新到 SQL Server 2016 中引入实时评分依赖于 R 和 Python 处理于 RevoScaleR、 MicrosoftML (R)、 revoscalepy，受 Microsoft 控制函数所代表的 CLR 库和microsoftml (Python)。 使用调用 CLR 库**sp_rxPredict**到存储的过程而不会调用 R 或 Python 运行时从任何支持的模型类型，生成分数。

[**本机计分**](../sql-native-scoring.md)是 SQL Server 2017 功能，作为一个本机实现C++库，但仅针对 RevoScaleR 和 revoscalepy 模型。 它是最快且更安全的方法，但支持一小部分相对于其他方法的函数。

## <a name="choose-a-scoring-method"></a>选择评分方法

平台要求通常指示要使用的评分方法。

| 产品版本和平台 | 方法 |
|------------------------------|-------------|
| Windows、 SQL Server 2017 Linux 和 Azure SQL 数据库上的 SQL Server 2017 | **本机计分**与 T-SQL 的预测 |
| SQL Server 2017 (仅 Windows) SQL Server 2016 R Services SP1 或更高版本 | **实时评分**sp\_rxPredict 存储过程 |

我们建议使用 PREDICT 函数的本机计分。 使用 sp\_rxPredict，需要启用 SQLCLR 集成。 在启用此选项之前，请考虑的安全隐患。

## <a name="serialization-and-storage"></a>序列化和存储

若要执行快速的评分方法之一使用一个模型，保存模型使用特殊的序列化的格式，已针对大小优化和评分效率。

+ 调用[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)要写入到支持的型号**原始**格式。
+ 调用[rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)来重建模型以在其他 R 代码，或若要查看的模型。

**使用 SQL**

从 SQL 代码中，你可以训练模型使用[sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，并直接插入在类型的列的表中已训练的模型**varbinary （max)**。 一个简单的示例，请参阅[在 R 中创建 preditive 模型](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

从 R 代码，调用[rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) RevoScaleR 包将模型直接写入数据库中的函数。 **RxWriteObject()** 函数可以检索从 ODBC 数据源 （如 SQL Server) 的 R 对象或对象写入 SQL Server。 该 API 只被现代性的简单键 / 值存储。
  
如果您使用此函数，请确保模型使用进行序列化[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)第一个。 然后，设置*序列化*中的参数**rxWriteObject**为 FALSE，以避免重复序列化步骤。

序列化成二进制格式的模型很有用，但如果你评分预测使用 R 和 Python 运行时环境可扩展性框架中不作要求。 可以将模型保存到文件的原始字节格式，然后从文件读取到 SQL Server。 如果您准备移动或复制环境之间的模型，此选项可能会很有用。

## <a name="scoring-in-related-products"></a>在相关产品中评分

如果使用的[独立服务器](r-server-standalone.md)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，可以有其他选择除了存储的过程和 T-SQL 的函数，用于快速生成预测。 独立服务器和机器学习服务器支持的概念*web 服务*代码部署。 你可以将捆绑 R 或 Python 预先训练模型作为 web 服务，在评估新的数据输入的运行时调用。 有关详细信息，请参阅以下文章：

+ [机器学习服务器中的 web 服务有哪些？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [操作化是什么？](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [将 Python 模型部署为 web 服务使用 azureml 模型管理 sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [将 R 代码块或实时模型发布为新的 web 服务](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [适用于 R 的 mrsdeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>另请参阅

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)