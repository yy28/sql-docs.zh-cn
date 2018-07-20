---
title: 使用 Python 模型中的训练和评分的 SQL |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 02ffd5a25c076ef5a65a6e3a998aae485e37d982
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085019"
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>在 SQL 中使用 Python 模型的训练和评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在中[上一课](wrap-python-in-tsql-stored-procedure.md)，您学习了使用 SQL 和 Python 的常见模式。 您学习了的 Python 代码应输出一个明确定义的数据帧，并可以选择输出多个标量或二进制变量。 介绍了应设计 SQL 存储过程以将正确类型的数据传递到 Python，并处理结果。

在本部分中，将使用此相同模式来训练某个模型已添加到 SQL Server 数据和将模型保存到 SQL Server 表：

+ 设计调用 Python 机器学习函数的存储的过程。
+ 存储的过程都需要从 SQL Server 要用于定型模型的数据。
+ 存储的过程输出的二进制变量为训练的模型。 
+ 通过向表插入变量的模型保存训练的模型。 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>创建存储的过程和 Python 模型定型

1. 在 SQL Server Management Studio 创建生成一个模型，该存储的过程中运行下面的代码。

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

2. 如果运行此命令时没有出错，新的存储的过程创建并添加到数据库。 可以在 Management Studio 中找到存储的过程**对象资源管理器**下**可编程性**。

3. 现在，运行存储的过程。

    ```sql
    EXEC generate_iris_model
    ```

    应显示一个错误，因为你尚未提供需要输入该存储过程。

    "过程或函数 'generate_iris_model' 需要参数 '\@trained_model，但未提供该。"

4. 若要生成具有所需的输入的模型并将其保存到表，需要一些附加的语句：

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 现在，尝试一次运行的模型生成代码。 

    你应收到错误:"违反了 PRIMARY KEY 约束不能在对象 dbo.iris_models 中插入重复键。 重复的键值是 (Naive Bayes)"。

    这是因为通过在"Naive Bayes"中手动键入作为 INSERT 语句的一部分提供的模型名称。 假设你打算创建大量的模型，每次运行使用不同的参数或不同的算法，应考虑设置元数据方案，以便您可以自动命名模型，更轻松地标识。

6. 若要避免此错误，您可以进行一些小改动对 SQL 的包装。 此示例通过追加当前日期和时间来生成唯一的模型名称：

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. 若要查看的模型，运行简单的 SELECT 语句。

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **结果**

    |model_name | model |
    |------|------|
    | Naive Bayes | 0x800363736B6C656172... |
    | Naive Bayes 2018 年 1 月 1 日上午 9:39 | 0x800363736B6C656172... |
    | Naive Bayes 年 2 月 1 日 2018 上午 10:51 | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>从模型生成分数

最后，让我们将此模型从表加载到一个变量，并将其传递回 Python 生成分数。

1. 运行以下代码以创建存储的过程执行评分。 

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

    存储的过程从表中获取朴素贝叶斯模型，并使用与模型相关联的函数生成评分。 在此示例中，存储的过程使用模型名称从表中获取的模型。 但是，具体取决于哪种元数据将保存使用模型，您还可以获取最新模型或模型最高的准确性。

2. 运行以下代码行以传递给执行评分的代码的存储过程的模型名称"Naive Bayes"。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    运行存储的过程时，它将返回 Python data.frame。 T-SQL 的这行指定返回的结果的架构： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    可以将结果插入到一个新表，或返回到应用程序。

    此示例变得简单使用从 Python 鸢尾花数据集的数据进行评分。 (请参阅行`iris_data[[1,2,3,4]])`。)但是，更常见的做法将运行 SQL 查询以获取新的数据，并将其传递到 Python 的`InputDataSet`。 

### <a name="remarks"></a>Remarks

如果您习惯于在 Python 中工作，你可能习惯于加载数据、 创建某些摘要和图形，然后为模型定型并全部放在同一个 250 行代码生成一些评分。

但是，如果你的目标是将 SQL Server 中的进程 （模型创建、 评分、 等） 进行操作，务必考虑方式，可以将该过程分到可以使用参数来修改的可重复步骤。 尽可能多地，你想要有明确的输入和输出映射到存储的过程输入和输出的存储过程中运行的 Python 代码。

此外，您通常可以通过从定型模型或生成评分的进程中分离数据浏览进程来提高性能。 

评分和培训流程可以经常优化通过利用 SQL Server 的功能，例如并行处理，或通过使用中的算法[revoscalepy](../python/what-is-revoscalepy.md)或[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)该支持流式处理和并行执行，而不是使用标准 Python 库。 

## <a name="next-lesson"></a>下一课

在最后一课中，从远程客户端，使用 SQL Server 作为计算上下文运行 Python 代码。 如果没有 Python 客户端，或不想运行 Python 的存储过程之外，此步骤是可选的。

+ [从 Python 客户端创建 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
