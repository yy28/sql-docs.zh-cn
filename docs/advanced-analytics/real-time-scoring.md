---
title: 使用 sp_rxPredict 存储过程的实时评分
description: 使用 sp_rxPredict 生成预测, 根据 SQL Server 上使用 R 编写的预先训练的模型对数据输入进行评分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b4284d77464597857eca500b4a8ad29e1f4d06ee
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469971"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>SQL Server 机器学习中的 sp_rxPredict 的实时评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

实时评分使用[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)系统存储过程和 CLR 扩展功能 SQL Server 来实现预测工作负荷的高性能预测或分数。 实时评分是语言不可知的, 在 R 或 Python 运行时间上无依赖项执行。 假设已使用 Microsoft 函数创建和训练了一个模型, 然后将其序列化为 SQL Server 中的二进制格式, 则可以使用实时评分在没有 R 或 Python 加载项的 SQL Server 实例上生成新数据输入的预测结果随.

## <a name="how-real-time-scoring-works"></a>实时评分的工作原理

对于基于 RevoScaleR 或 MicrosoftML 函数 (例如[rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML))](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)的特定模型类型, SQL Server 2017 和 SQL Server 2016 支持实时评分。 它使用本机C++库根据提供给以特殊二进制格式存储的机器学习模型的用户输入来生成评分。

因为训练的模型可用于评分而无需调用外部语言运行时, 所以减少了多个进程的系统开销。 这为生产计分方案支持更快的预测性能。 由于数据永远不会离开 SQL Server, 因此可以生成结果并将其插入到新表中, 而无需在 R 和 SQL 之间进行任何数据转换。

实时评分是一个多步骤过程:

1. 必须基于每个数据库启用执行评分的存储过程。
2. 以二进制格式加载预先训练的模型。
3. 提供要评分的新输入数据 (表格或单行) 作为模型的输入。
4. 若要生成分数, 请调用[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)存储过程。

## <a name="prerequisites"></a>系统必备

+ [启用 SQL SERVER CLR 集成](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ [启用实时计分](#bkmk_enableRtScoring)。

+ 必须使用支持的**rx**算法之一预先训练该模型。 对于 R, 适用`sp_rxPredict`于的实时评分适用于[RevoScaleR 和 MicrosoftML 支持的算法](#bkmk_rt_supported_algos)。 对于 Python, 请参阅[revoscalepy 和 microsoftml 支持的算法](#bkmk_py_supported_algos)

+ 使用[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) for R 和用于 Python 的[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)序列化模型。 已对这些序列化函数进行了优化, 以支持快速评分。

+ 将模型保存到要从中调用该模型的数据库引擎实例。 此实例不需要具有 R 或 Python 运行时扩展。

> [!Note]
> 实时评分目前经过优化, 可快速预测较小的数据集, 范围从几行到数百行。 在大型数据集上, 使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能会更快。

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>支持的算法

### <a name="python-algorithms-using-real-time-scoring"></a>使用实时评分的 Python 算法

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)\*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  标记为的\*模型还支持通过 PREDICT 函数的本机计分。

+ microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml 提供的转换

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>使用实时评分的 R 算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  标记为的\*模型还支持通过 PREDICT 函数的本机计分。

+ MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML 提供的转换

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不支持的模型类型

实时评分不使用解释器;因此, 在评分步骤中, 不支持任何可能需要解释器的功能。  这些情况可能包括：

  + 不支持使用`rxGlm`或`rxNaiveBayes`算法的模型。

  + 使用转换函数或包含转换的公式 (如<code>A ~ log(B)</code> ) 的模型不支持实时计分。 若要使用此类型的模型, 我们建议您在将数据传递到实时计分之前对输入数据执行转换。


## <a name="example-sprxpredict"></a>示例: sp_rxPredict

本部分介绍设置**实时**预测所需的步骤, 并提供有关如何从 t-sql 调用函数的 R 中的示例。

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>步骤 1. 启用实时评分过程

您必须为要用于评分的每个数据库启用此功能。 服务器管理员应运行包含在 RevoScaleR 包中的命令行实用程序 Registerrext.exe。

> [!NOTE]
> 若要运行实时评分, 需要在实例中启用 SQL CLR 功能;此外, 需要将该数据库标记为可信。 当你运行脚本时, 将为你执行这些操作。 但是, 在执行此操作之前, 请考虑其他安全隐患!

1. 打开提升的命令提示符, 并导航到 Registerrext.exe 所在的文件夹。 以下路径可用于默认安装:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 运行以下命令, 并将实例的名称和目标数据库替换为要启用扩展存储过程的位置:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    例如, 若要将扩展存储过程添加到默认实例的 CLRPredict 数据库中, 请键入:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    如果数据库在默认实例上, 则实例名称是可选的。 如果使用的是命名实例, 则必须指定实例名称。

3. Registerrext.exe 创建以下对象:

    + 受信任程序集
    + 存储过程`sp_rxPredict`
    + 一个新的数据库角色`rxpredict_users`。 数据库管理员可以使用此角色向使用实时评分功能的用户授予权限。

4. 添加需要运行`sp_rxPredict`到新角色的任何用户。

> [!NOTE]
> 
> SQL Server 2017 中提供了其他安全措施来防止 CLR 集成问题。 这些度量值还对此存储过程的使用产生了额外限制。 

### <a name="step-2-prepare-and-save-the-model"></a>步骤 2. 准备并保存模型

Sp\_rxPredict 所需的二进制格式与使用 PREDICT 函数所需的格式相同。 因此, 在 R 代码中包括对[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)的调用, 并确保指定`realtimeScoringOnly = TRUE`, 如下例所示:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步骤 3. 调用 sp_rxPredict

像对任何\_其他存储过程一样调用 sp rxPredict。 在当前版本中, 该存储过程仅采用两个参数 _\@_ : 模型为二进制格式的模型, 以及 _\@_ 用于计分的数据的 inputData, 定义为有效的 SQL 查询。

由于二进制格式与 PREDICT 函数使用的格式相同, 因此可以使用前面示例中的 "模型" 和 "数据表"。

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> 如果用于计分的\_输入数据未包含与模型的要求相匹配的列, 则对 sp rxPredict 的调用将失败。 目前仅支持以下 .NET 数据类型: double、float、short、ushort、long、ulong 和 string。
> 
> 因此, 你可能需要在输入数据中筛选掉不受支持的类型, 然后将其用于实时计分。
> 
> 有关相应的 SQL 类型的信息, 请参阅[sql-Clr 类型映射](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[映射 CLR 参数数据](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-real-time-scoring"></a>禁用实时评分

若要禁用实时评分功能, 请打开提升的命令提示符, 并运行以下命令:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>后续步骤

有关 SQL Server 中评分的更多背景信息, 请参阅[如何在 SQL Server 机器学习中生成预测](r/how-to-do-realtime-scoring.md)。
