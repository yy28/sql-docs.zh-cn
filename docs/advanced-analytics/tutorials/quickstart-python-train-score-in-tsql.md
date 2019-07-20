---
title: 使用存储过程进行定型和预测的 Python 模型快速入门
description: 在 SQL Server 存储过程中嵌入 Python 代码, 使用经典 Iris 数据集创建、定型和使用 Python 模型。 将训练的模型保存到 SQL Server, 并使用它来生成预测的结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c2c36c5aa81da098064885fd5b006d78494cd962
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345762"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>快速入门：使用中的存储过程创建、定型和使用 Python 模型 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此快速入门中, 你将创建并执行两个存储过程。 第一种模式使用经典 Iris 花卉数据集, 并生成一个简单的 Bayes 模型, 用于根据花朵特征预测 Iris 物种。 第二个过程用于评分。 它调用在第一个过程中生成的模型以输出一组预测。 通过在存储过程中放置代码, 其他存储过程和客户端应用程序可以对操作进行包含、重复使用和调用。 

完成本快速入门后, 你将了解:

> [!div class="checklist"]
> * 如何在存储过程中嵌入 Python 代码
> * 如何通过存储过程的输入将输入传递到代码
> * 如何使用存储过程操作模型

## <a name="prerequisites"></a>先决条件

之前的快速入门,[请验证 SQL Server 中是否存在 python](quickstart-python-verify.md), 并提供设置此快速入门所需的 Python 环境所需的信息和链接。

此练习中使用的示例数据是[**irissql**](demo-data-iris-in-sql.md)数据库。

## <a name="create-a-stored-procedure-that-generates-models"></a>创建用于生成模型的存储过程

SQL Server 开发中的常见模式是将可编程操作组织成不同的存储过程。 在此步骤中, 您将创建一个存储过程, 用于生成预测结果的模型。 

1. 在 Management Studio 中打开连接到**irissql**数据库的新查询窗口。 

    ```sql
    USE irissql
    GO
    ```

2. 复制以下代码以创建新的存储过程。 

   执行时, 此过程将调用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)来启动 Python 会话。 
   
   Python 代码所需的输入将作为输入参数传递到此存储过程。 根据机器学习算法的 Python **scikit-learn**库, 输出将是训练的模型。 

   此代码使用[**pickle**](https://docs.python.org/2/library/pickle.html)来序列化模型。 将使用**iris_data**表中来自0到4列的数据训练该模型。 
   
   在过程的第二部分中看到的参数阐明了数据输入和模型输出。 您希望在存储过程中运行的 Python 代码可以明确定义映射到在运行时传入的存储过程输入和输出的输入和输出。 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. 验证存储过程是否存在。 

   如果上一步骤中的 T-sql 脚本运行时未出现错误, 则会创建一个名为**generate_iris_model**的新存储过程, 并将其添加到**irissql**数据库。 在**可编程性**下, 你可以在 Management Studio 的**对象资源管理器**中找到存储过程。

## <a name="execute-the-procedure-to-create-and-train-models"></a>执行创建和训练模型的过程

在此步骤中, 执行该过程以运行嵌入式代码, 并将定型和序列化模型创建为输出。 为在 SQL Server 中重复使用而存储的模型将被序列化为字节流, 并存储在数据库表中的 VARBINARY (MAX) 列中。 创建、训练、序列化模型并将其保存到数据库后, 可通过其他过程或在评分工作负荷中[预测 t-sql](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)函数调用它。

1. 复制以下代码以执行该过程。 用于执行存储过程`EXEC`的特定语句位于第五行。

   此特定脚本删除同一名称 ("Naive Bayes") 的现有模型, 为通过重新运行同一过程创建的新模型腾出空间。 如果不删除模型, 则会出现一个错误, 指出该对象已存在。 模型存储在名为**iris_models**的表中。 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 验证是否已插入另一种返回模型列表的方法

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **结果**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>创建和执行存储过程以生成预测

现在, 您已创建、训练并保存了一个模型, 接下来请转到下一步: 创建用于生成预测的存储过程。 要执行此操作, 请调用 sp_execute_external_script 以启动 Python, 然后传入 Python 脚本, 该脚本加载您在上一个练习中创建的序列化模型, 然后将其数据输入提供给分数。

1. 运行以下代码以创建执行计分的存储过程。 在运行时, 此过程将加载一个二进制模型, 使用列`[1,2,3,4]`作为输入, 并将列`[0,5,6]`指定为输出。

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

2. 执行存储过程 (提供模型名称 "Naive Bayes"), 以便该过程知道要使用的模型。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    在运行该存储过程时, 它将返回 Python 数据。框架。 此 T-sql 行指定返回的结果的架构: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 您可以将结果插入到新表中, 或将其返回给应用程序。

    ![运行存储过程的结果集](media/train-score-using-python-NB-model-results.png)

    使用花卉特征作为输入, 结果为150的物种预测。 对于大多数观察, 预测的物种与实际物种匹配。

    通过使用 Python iris 数据集进行定型和评分, 此示例已变得简单。 更典型的方法是运行 SQL 查询以获取新数据, 并将该查询作为`InputDataSet`传递到 Python。 

## <a name="conclusion"></a>结束语

在此练习中, 您学习了如何创建专用于不同任务的存储过程, 其中每个存储过程都使用系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来启动 Python 进程。 Python 进程的输入将作为参数传递到 sp_execute_external 脚本。 Python 脚本本身和 SQL Server 数据库中的数据变量都作为输入传递。

通常, 只应计划将 SSMS 与精美的 Python 代码一起使用, 或者使用简单的 Python 代码来返回基于行的输出。 SSMS 支持查询语言 (例如 T-sql) 并返回平展行集。 如果你的代码生成类似于散点图或直方图的视觉输出, 则需要可以呈现图像的工具或最终用户应用程序。

对于那些用于编写各种操作的非独占脚本的某些 Python 开发人员, 将任务组织成单独的过程可能看起来不必要。 但定型和评分具有不同的用例。 通过分隔它们, 你可以将每个任务置于不同的计划, 并将权限作用域授予操作。

同样, 您还可以利用 SQL Server 的资源功能 (如并行处理、资源调控) 或编写脚本来使用支持流式处理和并行执行的[revoscalepy](../python/ref-py-revoscalepy.md)或[microsoftml](../python/ref-py-microsoftml.md)中的算法。 通过区分定型和评分, 可以针对特定工作负荷进行优化。

最后一个优点是可以使用参数修改进程。 在此练习中, 创建了模型 (在本示例中名为 "Naive Bayes") 的 Python 代码作为输入传递给在评分过程中调用该模型的另一个存储过程。 此练习只使用一个模型, 但您可以想像到计分任务中的模型参数化如何使该脚本更有用。

## <a name="next-steps"></a>后续步骤

如果你是适用于 Python 的 SQL 开发人员, 请查看本地使用 Python 代码的步骤和工具, 并能够将执行从本地会话转移到远程 SQL Server 实例。

> [!div class="nextstepaction"]
> [设置 Python 客户端工作站](../python/setup-python-client-tools-sql.md)。

