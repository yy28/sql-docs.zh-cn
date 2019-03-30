---
title: 实时评分使用 sp_rxPredict 存储过程的 SQL Server 机器学习服务
description: 生成使用 sp_rxPredict，评分对 SQL Server 上以 R 编写的预先训练模型的数据输入的预测。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 22f6c48aec0c9434b17ceda0a2b729f6e63bf136
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645469"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>使用 SQL Server 机器学习中 sp_rxPredict 实时评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

实时评分用途[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)系统存储过程和 CLR 扩展功能在 SQL Server 的高性能预测或预测的工作负荷中的评分。 实时评分是语言无关，并执行 R 或 Python 运行时间上没有依赖项。 假设创建和使用 Microsoft 函数训练，然后到 SQL Server 中的二进制格式序列化的模型，您可以使用实时评分来生成预测的结果上没有 R 或 Python 外接程序的 SQL Server 实例上的新数据输入安装。

## <a name="how-real-time-scoring-works"></a>如何实时评分的工作原理

实时评分对 RevoScaleR 或 MicrosoftML 函数如基于特定模型类型支持在 SQL Server 2016 和 SQL Server 2017 [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). 它使用本机 c + + 库来生成评分，根据用户输入提供给机器学习模型存储在特殊的二进制格式。

可用于训练的模型评分而无需调用外部语言运行时，由于减少了多个进程的开销。 这用于生产评分方案支持更快的预测性能。 因为数据不会离开 SQL Server，则可以生成结果，并将其插入到新表中不使用任何 R 和 SQL 之间的数据转换。

实时评分是一个多步骤过程：

1. 必须在每个数据库的基础上启用执行评分存储的过程。
2. 加载预先训练的模型以二进制格式。
3. 提供新的输入的数据进行评分，表格或单个行，作为模型的输入。
4. 若要生成评分，调用[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)存储过程。

## <a name="prerequisites"></a>先决条件

+ [启用 SQL Server CLR 集成](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ [启用实时评分](#bkmk_enableRtScoring)。

+ 必须事先使用某个受支持训练模型**rx**算法。 对于 R，实时与评分`sp_rxPredict`适用于[RevoScaleR 和 MicrosoftML 支持的算法](#bkmk_rt_supported_algos)。 对于 Python，请参阅[revoscalepy 和 microsoftml 支持的算法](#bkmk_py_supported_algos)

+ 模型使用进行序列化[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)对于 R，并[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)适用于 Python。 这些序列化函数已经过优化，以支持快速评分。

+ 将模型保存到你想要调用它的数据库引擎实例。 此实例不需要具有 R 或 Python 运行时扩展。

> [!Note]
> 针对快速预测对小型数据集，范围从少量的行到成千上万行的当前优化实时评分。 在大型数据集，使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能更快。

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>支持的算法

### <a name="python-algorithms-using-real-time-scoring"></a>Python 算法使用实时评分

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  模型标记为\*还支持使用预测函数的本机计分。

+ microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ 转换提供的 microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>R 算法使用实时评分

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  模型标记为\*还支持使用预测函数的本机计分。

+ MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ 转换提供的 MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不受支持的模型类型

实时评分不会使用解释器;因此，可能需要解释器的任何功能不支持在评分步骤。  这些情况可能包括：

  + 使用情况建模`rxGlm`或`rxNaiveBayes`算法不受支持。

  + 模型使用转换函数或公式包含一个转换，例如<code>A ~ log(B)</code>中实时评分不支持。 若要使用此类型的模型，我们建议将数据传递给实时评分之前，对输入数据执行转换。


## <a name="example-sprxpredict"></a>示例： sp_rxPredict

本部分介绍设置所需的步骤**实时**预测，并提供如何从 T-SQL 调用函数的 R 中的示例。

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>步骤 1. 启用实时评分过程

必须启用此功能为你想要使用进行评分的每个数据库。 服务器管理员应运行的命令行实用工具，RegisterRExt.exe，包含在 RevoScaleR 包。

> [!NOTE]
> 为了使实时评分工作，SQL CLR 功能需要启用实例; 中此外，数据库需要标记为可信。 当您运行该脚本时，为你执行这些操作。 但是，执行此操作之前考虑的其他安全隐患 ！

1. 打开提升的命令提示符，并导航到 RegisterRExt.exe 所在的文件夹。 可以在默认安装中使用以下路径：
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 运行以下命令，替换为你的实例和你想要启用的扩展存储的过程的目标数据库名称：

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    例如，若要将扩展存储的过程添加到默认实例上的 CLRPredict 数据库，请键入：

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    如果数据库是默认实例上可选实例名。 如果使用的命名的实例，必须指定实例名称。

3. RegisterRExt.exe 创建以下对象：

    + 受信任的程序集
    + 存储的过程 `sp_rxPredict`
    + 新的数据库角色， `rxpredict_users`。 数据库管理员可以使用此角色向使用实时评分功能的用户授予权限。

4. 添加需要运行的任何用户`sp_rxPredict`到新的角色。

> [!NOTE]
> 
> 在 SQL Server 2017 中，其他安全措施到位以防止使用 CLR 集成的问题。 这些度量值有附加限制在使用此存储的过程。 

### <a name="step-2-prepare-and-save-the-model"></a>步骤 2. 准备并保存模型

Sp 所需的二进制格式\_rxPredict 是使用 PREDICT 函数所需的格式相同。 因此，在 R 代码中，包括对[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，并确保指定`realtimeScoringOnly = TRUE`，如下例所示：

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步骤 3. Call sp_rxPredict

Sp 调用\_rxPredict 作为您像对任何其他存储过程。 在当前版本中，存储的过程将只有两个参数： _\@模型_中的二进制格式，模型和 _\@inputData_要计分中，使用的数据定义为有效的 SQL 查询。

由于二进制格式是相同的由 PREDICT 函数，可以使用从前面的示例模型和数据的表。

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
> Sp 调用\_rxPredict 失败如果评分的输入的数据不包括与该模型的要求匹配的列。 目前，支持仅以下.NET 数据类型： 双精度型、 float、 short、 ushort、 long、 ulong 和字符串。
> 
> 因此，您可能需要筛选出输入数据中不支持的类型，然后再使用它进行实时评分。
> 
> 有关相应 SQL 类型的信息，请参阅[SQL-CLR 类型映射](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[映射 CLR 参数数据](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-real-time-scoring"></a>禁用实时评分

若要禁用实时评分的功能，打开提升的命令提示符，并运行以下命令： `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>后续步骤

有关更多背景信息评分在 SQL Server 中，请参阅[如何在 SQL Server 机器学习中生成预测](r/how-to-do-realtime-scoring.md)。
