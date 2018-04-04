---
title: 如何执行实时评分或在 SQL Server 中的本机评分 |Microsoft 文档
ms.custom: ''
ms.date: 11/09/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 186ead48ffe33eb8b9dc169041aaf78212a36b0a
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>如何执行实时评分或在 SQL Server 中的本机评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

这篇文章提供有关如何执行实时评分和 SQL Server 2017 和 SQL Server 2016 中的本机评分功能说明和示例代码。 同时实时评分和本机评分的目标是提高在小的批处理计分操作的性能。

同时实时评分和本机评分旨在让你使用机器学习模型，而无需安装。你需要做是获取预先训练的模型的兼容格式，并将其保存在 SQL Server 数据库中。

## <a name="choosing-a-scoring-method"></a>选择评分方法

快速的批处理预测支持以下选项：

+ **本机评分**： 在 SQL Server 2017 T-SQL 的预测函数
+ **实时评分**： 使用 sp\_rxPredict 存储过程在 SQL Server 2016 或 SQL Server 自 2017 年。

> [!NOTE]
> 在 SQL Server 2017 中建议的预测函数的使用。
> 若要使用 sp\_rxPredict 要求你启用 SQLCLR 集成。 在启用此选项之前，请考虑的安全隐患。

准备模型，然后生成评分的整个过程是类似：

1. 创建使用受支持的算法的模型。
2. 序列化模型时使用的特殊的二进制格式。
3. 使模型可供 SQL Server。 通常这意味着在 SQL Server 表中存储的序列化的模型。
4. 调用的函数或存储的过程，并传递的模型和输入的数据。

### <a name="requirements"></a>需求

+ 预测函数也可在所有版本的 SQL Server 2017 默认处于启用状态。 不需要安装 R 或启用额外功能。

+ 如果使用 sp\_rxPredict，执行一些其他步骤所需。 请参阅[启用实时评分](#bkmk_enableRtScoring)。

+ 在此期间，只有 RevoScaleR 和 MicrosoftML 可以创建兼容的模型。 在将来可能会提供其他模型类型。 当前支持的算法的列表，请参阅[实时评分](../real-time-scoring.md)。

### <a name="serialization-and-storage"></a>序列化和存储

若要使用的任一快速评分选项使用的模型，保存模型使用特殊的序列化的格式，已经过优化，大小和评分效率。

+ 调用`rxSerializeModel`要写入到支持的模型**原始**格式。
+ 调用`rxUnserializeModel`若要重建模型以在其他 R 代码，或查看模型。

有关详细信息，请参阅[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)。

**使用 SQL**

从 SQL 代码，你可以训练模型使用`sp_execute_external_script`，并直接将训练的模型插入到表，列中的类型**varbinary （max)**。

一个简单的示例，请参阅[本教程](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

从 R 代码中，有两种方法可以将模型保存到表：

+ 调用`rxWriteObject`函数，从 RevoScaleR 包，该模型直接写入数据库。

  `rxWriteObject()`函数可以从类似于 SQL Server ODBC 数据源中检索 R 对象或对象写入 SQL Server。 API 仿效简单的键-值存储。
  
  如果使用此函数时，一定要序列化模型首先使用新的序列化函数。 然后，设置*序列化*中的参数`rxWriteObject`为 FALSE，以避免重复序列化步骤。

+ 你可以还将模型保存到文件的原始格式，然后从文件读取到 SQL Server。 如果您准备移动或复制环境之间的模型，此选项可能会很有用。

## <a name="native-scoring-with-predict"></a>本机与预测评分

在此示例中，你将创建模型时，，，然后从 T-SQL 调用实时预测函数。

### <a name="step-1-prepare-and-save-the-model"></a>步骤 1. 准备和保存模型

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

使用以下语句以填充数据的数据表格**iris**数据集。

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

下面的代码创建基于模型**iris**数据集并将其保存到名为的表**模型**。

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
> 请务必使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) RevoScaleR 保存模型的函数。 标准 R`serialize`函数无法生成所需的格式。

你可以运行类似以下内容以查看存储的模型中的二进制格式的语句：

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步骤 2. 对模型运行预测

以下简单预测语句从决策树模型使用获取分类**本机评分**函数。 它预测 iris 种类基于您提供的特性、 花瓣长度和宽度。

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

如果你收到错误，"执行期间出现错误的函数预测。 模型已损坏或无效"，则通常意味着在你的查询没有返回一个模型。 检查是否正确，键入模型名称或模型表是否为空。

> [!NOTE]
> 因为这些列和值返回**预测**可以根据模型类型而变化，则必须使用定义返回的数据的架构**WITH**子句。

## <a name="realtime-scoring-with-sprxpredict"></a>实时 sp_rxPredict 评分

本部分介绍设置所需的步骤**实时**预测，并提供了如何从 T-SQL 的调用函数的一个示例。

### <a name ="bkmk_enableRtScoring"></a> 步骤 1。 启用实时评分过程

必须启用此功能，你想要用于评分的每个数据库。 服务器管理员应运行的命令行实用工具，RegisterRExt.exe，包含在 RevoScaleR 包。

> [!NOTE]
> 为了使实时评分来工作，SQL CLR 功能需要启用实例; 中此外，数据库需要标记为可信。 运行脚本时，为你执行这些操作。 但是，执行此操作之前考虑的其他安全隐患 ！

1. 打开提升的命令提示符，并导航到 RegisterRExt.exe 所在的文件夹。 默认安装中，可以使用以下路径：
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 运行以下命令，替换为你的实例和目标数据库在你想要启用扩展存储的过程的名称：

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    例如，若要将扩展存储的过程添加到默认实例上的 CLRPredict 数据库，请键入：

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    实例名称是可选的如果数据库位于默认实例上。 如果你使用的命名的实例，必须指定实例名称。

3. RegisterRExt.exe 创建以下对象：

    + 受信任的程序集
    + 存储的过程 `sp_rxPredict`
    + 新的数据库角色， `rxpredict_users`。 数据库管理员可以使用此角色向使用实时评分功能的用户授予权限。

4. 添加需要运行的任何用户`sp_rxPredict`到新的角色。

> [!NOTE]
> 
> 在 SQL Server 自 2017 年，附加的安全措施是到位以避免使用 CLR 集成的问题。 这些度量值会施加额外的使用限制以及此存储过程。 

### <a name="step-2-prepare-and-save-the-model"></a>步骤 2. 准备和保存模型

Sp 所需的二进制格式\_rxPredict 等同于使用预测函数所需的格式。 因此，在 R 代码中，包括调用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，并且请务必指定`realtimeScoringOnly = TRUE`，如下例所示：

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步骤 3. 调用 sp_rxPredict

Sp 调用\_rxPredict 作为你像对任何其他存储过程。 在当前版本中，该存储的过程将只有两个参数： _@model_为二进制格式中的模型和_@inputData_中评分，使用的数据定义为有效的 SQL 查询.

由于二进制格式是相同的预测函数使用，你可以使用模型和数据从前面的示例表。

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
> Sp 调用\_rxPredict 失败如果评分的输入的数据不包含匹配的模型的要求的列。 目前，支持只能使用以下的.NET 数据类型： 双精度型、 float、 short、 ushort，long、 ulong 和字符串。
> 
> 因此，你可能需要使用实时评分之前筛选出你输入的数据中不支持的类型。
> 
> 有关相应 SQL 类型的信息，请参阅[SQL CLR 类型映射](https://msdn.microsoft.com/library/bb386947.aspx)或[映射 CLR 参数数据](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-realtime-scoring"></a>禁用实时评分

若要禁用实时评分功能，打开提升的命令提示符，并运行以下命令： `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>在 Microsoft R Server 或机器学习 Server 评分的实时

机器学习服务器支持从作为 web 服务发布的模型评分的分布式的实时。 有关详细信息，请参阅以下文章：

+ [机器学习服务器中的 web 服务有哪些？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什么是操作化？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [将 Python 模型部署为具有 azureml 模型管理 sdk 的 web 服务](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [将 R 代码块或实时模型发布为新的 web 服务](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [mrsdeploy 包](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
