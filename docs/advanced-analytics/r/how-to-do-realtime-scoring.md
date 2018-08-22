---
title: 如何执行实时评分或在 SQL Server 机器学习中的本机计分 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dfea308f268d666ce070c21a7dd9afa513f95406
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "40392058"
---
# <a name="how-to-perform-real-time-scoring-or-native-scoring-in-sql-server"></a>如何执行实时评分或在 SQL Server 中的本机计分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文演示如何在 SQL Server 中的两种方法，用于预测结果： 在近实时使用预先训练的模型编写的。实时评分和本机计分都旨在使你可以使用机器学习模型，而无需安装。在兼容的格式-保存到 SQL Server 数据库-提供预先训练的模型可以使用标准数据访问技术来快速生成预测得分的新输入。

## <a name="choose-a-scoring-method"></a>选择评分方法

快速的批处理预测支持以下选项：

+ **本机计分**： 在 SQL Server 2017 Windows、 SQL Server 2017 Linux 和 Azure SQL 数据库 T-SQL 的预测函数。
+ **实时评分**： 使用 sp\_rxPredict 存储过程在 SQL Server 2016 或 SQL Server 2017 (仅 Windows) 中。

> [!NOTE]
> 在 SQL Server 2017 中建议使用 PREDICT 函数。
> 若要使用 sp\_rxPredict，需要启用 SQLCLR 集成。 在启用此选项之前，请考虑的安全隐患。

准备模型，然后生成评分的整个过程是类似：

1. 创建使用受支持的算法的模型。
2. 序列化在模型中使用特殊的二进制格式。
3. 使模型可供 SQL Server。 通常这意味着在 SQL Server 表中存储的序列化的模型。
4. 调用的函数或存储的过程，并传递的模型和输入的数据。

### <a name="requirements"></a>要求

+ PREDICT 函数可在所有版本的 SQL Server 2017 中，并且默认情况下启用。 不需要安装 R 或启用其他功能。

+ 如果使用 sp\_rxPredict，所需执行一些其他步骤。 请参阅[启用实时评分](#bkmk_enableRtScoring)。

+ 在此期间，只有 RevoScaleR 和 MicrosoftML 可创建兼容型号。 在将来可能会提供其他模型类型。 当前支持的算法的列表，请参阅[实时评分](../real-time-scoring.md)。

### <a name="serialization-and-storage"></a>序列化和存储

若要执行快速的评分方法之一使用一个模型，保存模型使用特殊的序列化的格式，已针对大小优化和评分效率。

+ 调用`rxSerializeModel`写入到支持的型号**原始**格式。
+ 调用`rxUnserializeModel`来重建模型以在其他 R 代码，或若要查看的模型。

有关详细信息，请参阅[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)。

**使用 SQL**

从 SQL 代码中，你可以训练模型使用`sp_execute_external_script`，并将已训练的模型直接插入在类型的列的表中**varbinary （max)**。

一个简单的示例，请参阅[本教程](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

从 R 代码中，有两种方法将模型保存到表：

+ 调用`rxWriteObject`函数，RevoScaleR 包，将模型直接写入数据库中的。

  `rxWriteObject()`函数可以检索从 ODBC 数据源 （如 SQL Server) 的 R 对象或对象写入 SQL Server。 该 API 只被现代性的简单键 / 值存储。
  
  如果使用此函数，请务必首先使用新的序列化函数将模型序列化。 然后，设置*序列化*中的参数`rxWriteObject`为 FALSE，以避免重复序列化步骤。

+ 可以还将该模型保存到文件原始格式，然后从文件读取到 SQL Server。 如果您准备移动或复制环境之间的模型，此选项可能会很有用。

## <a name="native-scoring-with-predict"></a>本机计分功能与预测

在此示例中，您创建模型，，，然后从 T-SQL 调用实时预测函数。

### <a name="step-1-prepare-and-save-the-model"></a>步骤 1. 准备并保存模型

运行以下代码以创建示例数据库和所需的表。

```SQL
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

使用以下语句来填充数据的数据表格**鸢尾花**数据集。

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

现在，创建用于存储模型的表。

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

以下代码将创建一个基于模型**iris**数据集并将其保存到名为表**模型**。

```SQL
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> 请务必使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) RevoScaleR 保存模型的函数。 标准 R`serialize`函数不能生成所需的格式。

可以运行以下命令以查看存储的模型以二进制格式之类的语句：

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步骤 2. 对模型运行预测

下面的简单预测语句从决策树模型使用获取分类**本机计分**函数。 它预测鸢尾花种类基于你提供的属性、 花瓣长度和宽度。

```SQL
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

如果收到错误，"执行期间出现错误的函数 PREDICT。 模型已损坏或无效"，这通常意味着您的查询未返回一个模型。 检查是否键入模型名称正确，或者如果模型表为空。

> [!NOTE]
> 因为返回的列和值**PREDICT**因模型类型而异，则必须使用定义返回的数据的架构**WITH**子句。

## <a name="real-time-scoring-with-sprxpredict"></a>使用 sp_rxPredict 实时评分

本部分介绍设置所需的步骤**实时**预测，并提供如何从 T-SQL 调用函数的示例。

### <a name ="bkmk_enableRtScoring"></a> 第 1 步。 启用实时评分过程

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

### <a name="step-3-call-sprxpredict"></a>步骤 3. 调用 sp_rxPredict

Sp 调用\_rxPredict 作为您像对任何其他存储过程。 在当前版本中，存储的过程将只有两个参数： _\@模型_中的二进制格式，模型和 _\@inputData_要计分中，使用的数据定义为有效的 SQL 查询。

由于二进制格式是相同的由 PREDICT 函数，可以使用从前面的示例模型和数据的表。

```SQL
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

## <a name="real-time-scoring-in-other-microsoft-product"></a>在其他 Microsoft 产品中的实时评分

如果使用独立服务器或 Microsoft 机器学习服务器而不 SQL Server 数据库内分析，则必须除了存储的过程和 T-SQL 的函数，用于生成预测的其他选项。

独立服务器和机器学习服务器支持的概念*web 服务*代码部署。 你可以将捆绑 R 或 Python 预先训练模型作为 web 服务，在评估新的数据输入的运行时调用。 有关详细信息，请参阅以下文章：

+ [机器学习服务器中的 web 服务有哪些？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [操作化是什么？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [将 Python 模型部署为 web 服务使用 azureml 模型管理 sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [将 R 代码块或实时模型发布为新的 web 服务](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [适用于 R 的 mrsdeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
