---
title: 使用 SQL 来进行定型和评分中的 Python 模型 |Microsoft 文档
titleSuffix: SQL Server
ms.custom: ''
ms.date: 02/28/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 976ccb21ed125bb65ba52eb05fd8b08664061a31
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>使用在 SQL 中的 Python 模型进行定型集和评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在[上一课](wrap-python-in-tsql-stored-procedure.md)，您学习了使用 Python 以及 SQL 的通用模式。 你已了解你的 Python 代码应输出一个明确定义的 data.frame，和可以有选择性地输出多个标量或 binary 变量。 你已了解应设计 SQL 存储过程以将正确的类型的数据传递给 Python，并处理结果。

在本部分中，可以使用此相同模式来训练某个模型已添加到 SQL Server，对数据和将模型保存到的 SQL Server 表：

+ 设计一个存储的过程调用 Python 机器学习函数。
+ 存储的过程需要从 SQL Server 以使用在定型模型的数据。
+ 存储的过程作为二进制变量输出训练的模型。 
+ 通过将插入一个表的变量的模型保存训练的模型。 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>创建存储的过程并定型 Python 模型

1. 在 SQL Server Management Studio 创建的存储的过程的生成一个模型中运行下面的代码。

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

2. 如果此命令可以正常运行，是创建新的存储的过程并将其添加到数据库。 你可以在 Management Studio 找到存储的过程**对象资源管理器**下**可编程性**。

3. 现在运行存储的过程。

    ```sql
    EXEC generate_iris_model
    ```

    你应收到错误，因为尚未提供输入存储过程要求。

    "过程或函数 generate_iris_model 需要参数@trained_model，但未提供该。"

4. 若要生成具有所需的输入模型并将其保存到表，需要某些其他语句：

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 现在，请尝试再次运行模型生成代码。 

    你应收到错误:"PRIMARY KEY 约束冲突无法在对象 dbo.iris_models 中插入重复键。 重复的键值是 (Naive Bayes)"。

    这是因为通过手动输入"Naive Bayes"中作为 INSERT 语句的一部分提供模型名称。 假设你打算创建大量模型，并将在每次运行使用不同的参数或不同的算法，应考虑设置元数据方案，以便您可以自动命名模型，更轻松地标识它们。

6. 若要获取解决此错误，你可以为 SQL 包装一些小改动。 此示例生成唯一的模型名称后面追加当前日期和时间：

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. 若要查看模型，请运行简单的 SELECT 语句。

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **结果**

    |model_name | model |
    |------|------|
    | Naive Bayes | 0x800363736B6C656172... |
    | Naive Bayes 年 1 月 01 2018 上午 9:39 | 0x800363736B6C656172... |
    | Naive Bayes 年 2 月 01 2018 10:51 AM | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>从模型生成评分

最后，让我们从表的此模型加载到变量中，并将其传递回 Python 生成评分。

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

    存储的过程获取表中的 Naïve Bayes 模型，并使用与模型关联的函数来生成评分。 在此示例中，存储的过程使用的模型名称从表中获取的模型。 但是，具体取决于哪种类型的元数据要保存使用模型，你可能还可以获取的最新模型的最高的精度。

2. 运行以下代码行中，以将"Naive Bayes"的型号名称传递给存储过程执行评分的代码。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    运行存储的过程时，它将返回 Python data.frame。 T-SQL 此行指定返回的结果的架构： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    你可以将结果插入到一个新表，或将它们返回到应用程序。

    此示例已发出简单评分使用 Python iris 数据集的数据。 (请参阅行`iris_data[[1,2,3,4]])`。)但是，更常见的做法将运行 SQL 查询，以便获取新的数据，并传递到作为 Python `InputDataSet`。 

### <a name="remarks"></a>注释

如果你习惯于在 Python 中工作，你可能会习惯于加载数据、 创建一些摘要和关系图，然后定型模型和代码的相同 250 行中所有生成一些评分。

但是，如果你的目标是使 SQL Server 中的过程 （创建模型，评分、 等），务必考虑到可使用参数来修改的可重复步骤可以分隔过程的方式。 尽可能多地，你想在映射到存储的过程输入和输出的输入和输出已明确定义的存储过程中运行的 Python 代码。

此外，你通常可以通过从定型模型或生成评分的进程中分离数据浏览过程来提高性能。 

评分和培训进程可以通常优化通过利用功能的 SQL Server，如并行处理，或通过使用中的算法[revoscalepy](../python/what-is-revoscalepy.md)或[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)该支持流式处理和并行执行，而不是使用标准的 Python 库。 

## <a name="next-lesson"></a>下一课

在最终的课中，你可以从远程客户端，使用 SQL Server 作为计算上下文运行 Python 代码。 此步骤是可选的，如果你没有 Python 客户端，或不想要在存储过程以外运行 Python。

+ [从 Python 客户端创建 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
