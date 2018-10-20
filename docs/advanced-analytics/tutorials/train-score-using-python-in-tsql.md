---
title: 使用 SQL Server 中的 Python 模型训练和预测 |Microsoft Docs
description: 创建并使用 Python 和经典鸢尾花数据集训练模型。 将模型保存到 SQL Server，然后使用它来生成预测的结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 839bcecdeaf7b5e2a7ea1297fe941353bffed20e
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461833"
---
# <a name="use-a-python-model-in-sql-server-for-training-and-scoring"></a>使用 SQL Server 中的 Python 模型的训练和评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 Python 此练习中，了解创建、 训练，以及使用 SQL Server 中的模型的常见模式。 本练习中创建两个存储的过程。 第一个将生成一个朴素贝叶斯模型来预测鸢尾花物种花卉特征。 第二个过程是进行评分。 它将调用输出一组预测的第一个步骤中生成的模型。 通过逐步完成此练习中，你将了解到 SQL Server 数据库引擎实例上执行 Python 代码中不可或缺的基本技术。

在此练习中使用的示例数据[鸢尾花数据集](demo-data-iris-in-sql.md)中**irissql**数据库。

## <a name="create-a-model-using-a-sproc"></a>使用存储过程创建模型

1. 打开 Management Studio 中新的查询窗口连接到**irissql**数据库。 

    ```sql
    USE irissql
    GO
    ```

2. 若要创建的存储的过程生成并定型模型的一个新查询窗口中运行下面的代码。 序列化为字节流和存储在数据库表中的 varbinary （max） 列中以供重复使用 SQL Server 中存储的模型。 创建模型后，定型、 序列化，并保存到数据库，它可以调用其他过程或评分工作负荷中的预测 T-SQL 函数。

   此代码使用 pickle 要序列化的模型和 scikit 提供的朴素贝叶斯算法。 将使用从 0 到 4 列中的数据训练模型**iris_data**表。 您在该过程的第二部分中看到的参数清楚地讲述数据输入和模型输出。 

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

3. 验证存储的过程存在。 如果在上一步中的 T-SQL 脚本运行正常，一个新的存储过程调用**generate_iris_model**被创建并添加到**irissql**数据库。 可以在 Management Studio 中找到存储的过程**对象资源管理器**下**可编程性**。

## <a name="execute-the-sproc-to-create-and-train-models"></a>执行存储过程来创建和训练模型

1. 创建此存储的过程后，运行以下代码来执行它。 用于执行存储的过程的特定语句是`EXEC`第五个行上。

   此特定脚本中删除现有的同名 ("Naive Bayes") 以容纳所通过重新运行相同的过程创建新的模型。 而不执行模型删除出错时指出该对象已存在。 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes '
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 在输出区域中查看结果。 该脚本包括显示模型存在的 SELECT 语句。 另一种方法来返回模型的列表是`SELECT * FROM iris_models`中**irissql**。

    **结果**

    |   | （无列名 |
    |---|-----------------|
    | 1 | Naive Bayes     | 


## <a name="create-and-execute-a-sproc-for-generating-predictions"></a>创建和执行存储过程用于生成预测

现在，已创建、 定型，并保存了该模型，转到下一步： 创建存储的过程来生成预测。 将通过调用 sp_execute_external_script 来启动 Python，然后将其传递中加载序列化的模型在上一练习中创建，然后为其提供要评分的数据输入的 Python 脚本来执行此操作。

1. 运行以下代码以创建存储的过程执行评分。 在运行时，此过程将加载二进制模型，使用列`[1,2,3,4]`作为输入，，指定列`[0,5,6]`作为输出。

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
    OutputDataSet = iris_data[[0,5,6]] 
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

2. 执行存储的过程，为模型名称"Naive Bayes"提供，以便让该过程知道要使用的模型。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    运行存储的过程时，它将返回 Python data.frame。 T-SQL 的这行指定返回的结果的架构： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 可以将结果插入到一个新表，或返回到应用程序。

    ![来自运行存储的过程的结果集](media/train-score-using-python-NB-model-results.png)

    结果是有关使用花卉特征作为输入的物种 150 预测。 对于的观测值的大多数，预测的物种匹配实际的种类。

    此示例变得简单通过 Python 鸢尾花数据集用于训练和评分。 更典型的方法将涉及在运行 SQL 查询以获取新数据，并将其传递到 Python 的`InputDataSet`。 

## <a name="conclusion"></a>结语

在此练习中，您学习了如何创建存储的过程，以不同的任务，其中每个存储的过程使用系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)启动 Python 进程。 到 Python 进程的输入作为参数传递给 sp_execute_external 脚本。 Python 脚本本身和 SQL Server 数据库中的数据变量作为输入传递。

如果您习惯于在 Python 中工作，你可能习惯于加载数据、 创建某些摘要和图形，然后为模型定型并全部放在同一个 250 行代码生成一些评分。 本文从惯用方法不同，通过组织到单独的过程操作。 在多个级别上，这种做法非常有用。

一个好处是可以分隔成可以使用参数来修改的可重复步骤的过程。 尽可能多地，您希望在存储过程中要有明确的输入和输出映射到存储的过程的输入和输出，可在运行时中传递运行 Python 代码。 在此练习中，创建模型 （名为"Naive Bayes"在此示例中） 的 Python 代码作为第二个存储过程，用于在评分过程中调用模型的输入传递。

第二个好处是定型和评分的进程可以通过利用 SQL Server 的功能，例如并行处理，资源调控功能，或使用中的算法优化[revoscalepy](../python/what-is-revoscalepy.md)或[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)的支持流式处理和并行执行。 通过将训练和评分，可以面向特定的工作负荷的优化。

## <a name="next-steps"></a>后续步骤

前面的教程侧重于本地执行。 但是，您也可以运行 Python 代码从客户端工作站上，使用 SQL Server 作为远程计算上下文。 有关如何设置连接到 SQL Server 的客户端工作站的详细信息，请参阅[设置 Python 客户端工具](../python/setup-python-client-tools-sql.md)。

+ [从 Python 客户端创建 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
