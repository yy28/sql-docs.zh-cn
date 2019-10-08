---
title: 在 Python 中创建和评分预测模型
titleSuffix: SQL Server Machine Learning Services
description: 使用 SQL Server 机器学习服务在 Python 中创建一个简单的预测模型，然后使用新数据预测结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 504b37002bedf0e73cfefe0aeb36faf2cca45bfe
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006014"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>快速入门：使用 SQL Server 机器学习服务在 Python 中创建和评分预测模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，你将使用 Python 创建和训练预测模型，将该模型保存到 SQL Server 实例中的表，然后使用该模型从使用[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)的新数据中预测值。

您将创建并执行在 SQL 中运行的两个存储过程。 第一种模式使用经典 Iris 花卉数据集，并生成一个简单的 Bayes 模型，用于根据花朵特征预测 Iris 物种。 第二个过程用于评分-它调用在第一个过程中生成的模型，以便基于新数据输出一组预测。 通过在存储过程中放置代码，其他存储过程和客户端应用程序可以对操作进行包含、重复使用和调用。

完成本快速入门后，你将了解：

> [!div class="checklist"]
> - 如何在存储过程中嵌入 Python 代码
> - 如何通过存储过程的输入将输入传递到代码
> - 如何使用存储过程操作模型

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装了 Python 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 的实例。

- 还需要一个用于运行包含 Python 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

- 此练习中使用的示例数据是 Iris 示例数据。 按照[Iris 演示数据](demo-data-iris-in-sql.md)中的说明创建示例数据库**irissql**。

## <a name="create-a-stored-procedure-that-generates-models"></a>创建用于生成模型的存储过程

在此步骤中，你将创建一个存储过程，用于生成预测结果的模型。

1. 在 SSMS 中打开一个连接到**irissql**数据库的新查询窗口。 

    ```sql
    USE irissql
    GO
    ```

1. 复制以下代码以创建新的存储过程。

   执行时，此过程将调用[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来启动 Python 会话。 
   
   Python 代码所需的输入将作为输入参数传递到此存储过程。 根据机器学习算法的 Python **scikit-learn**库，输出将是训练的模型。 

   此代码使用[**pickle**](https://docs.python.org/2/library/pickle.html)来序列化模型。 将使用**iris_data**表中来自0到4列的数据训练该模型。 
   
   在过程的第二部分中看到的参数阐明了数据输入和模型输出。 您希望在存储过程中运行的 Python 代码可以明确定义映射到在运行时传入的存储过程输入和输出的输入和输出。

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
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

1. 验证存储过程是否存在。 

   如果上一步骤中的 T-sql 脚本运行时未出现错误，则会创建一个名为**generate_iris_model**的新存储过程，并将其添加到**irissql**数据库。 可以在 "**可编程性**" 下的 SSMS**对象资源管理器**中找到存储过程。

## <a name="execute-the-procedure-to-create-and-train-models"></a>执行创建和训练模型的过程

在此步骤中，您将执行该过程以运行嵌入式代码，并将定型和序列化模型创建为输出。 

为在 SQL Server 中重复使用而存储的模型将被序列化为字节流，并存储在数据库表中的 VARBINARY （MAX）列中。 创建、训练、序列化模型并将其保存到数据库后，可通过其他过程或在评分工作负荷中[预测 t-sql](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)函数调用它。

1. 运行以下脚本以执行该过程。 用于执行存储过程的特定语句在第四行 @no__t 为0。

   此特定脚本删除同一名称（"Naive Bayes"）的现有模型，为通过重新运行同一过程创建的新模型腾出空间。 如果不删除模型，则会出现一个错误，指出该对象已存在。 模型存储在名为**iris_models** **的表**中。

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. 验证是否已插入该模型。

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **结果**

    | model_name  | 模型 |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>创建和执行存储过程以生成预测

现在，您已创建、训练并保存了一个模型，接下来请转到下一步：创建用于生成预测的存储过程。 要执行此操作，需要调用 `sp_execute_external_script` 来运行一个 Python 脚本，该脚本将加载序列化模型并将新的数据输入提供给分数。

1. 运行以下代码以创建执行计分的存储过程。 在运行时，此过程将加载二进制模型，使用列 `[1,2,3,4]` 作为输入，并将 @no__t 列指定为-1 作为输出。

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
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
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. 执行存储过程（提供模型名称 "Naive Bayes"），以便该过程知道要使用的模型。

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   在运行该存储过程时，它将返回 Python 数据。框架。 此 T-sql 行指定返回的结果的架构： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 您可以将结果插入到新表中，或将其返回给应用程序。

   ![运行存储过程的结果集](media/train-score-using-python-NB-model-results.png)

   使用花卉特征作为输入，结果为150的物种预测。 对于大多数观察，预测的物种与实际物种匹配。

   通过使用 Python iris 数据集进行定型和评分，此示例已变得简单。 更典型的方法是运行 SQL 查询以获取新数据，并将其作为 @no__t 传递到 Python。

## <a name="conclusion"></a>结束语

在此练习中，您学习了如何创建专用于不同任务的存储过程，其中每个存储过程使用系统存储过程 `sp_execute_external_script` 来启动 Python 进程。 Python 进程的输入将作为参数传递到 `sp_execute_external`。 Python 脚本本身和 SQL Server 数据库中的数据变量都作为输入传递。

通常，只应计划将 SSMS 与精美的 Python 代码一起使用，或者使用简单的 Python 代码来返回基于行的输出。 SSMS 支持查询语言（例如 T-sql）并返回平展行集。 如果你的代码生成类似于散点图或直方图的视觉输出，则需要可以呈现图像的工具或最终用户应用程序。

对于那些用于编写各种操作的非独占脚本的某些 Python 开发人员，将任务组织成单独的过程可能看起来不必要。 但定型和评分具有不同的用例。 通过分隔它们，可以将每个任务置于不同的计划，并将每个操作的权限作用域。

同样，还可以利用 SQL Server 的资源功能（如并行处理、资源调控）或编写脚本来使用支持流式处理和并行执行的[microsoftml](../python/ref-py-microsoftml.md)中的算法。 通过区分定型和评分，可以针对特定工作负荷进行优化。

最后一个优点是可以使用参数修改进程。 在此练习中，创建了模型（在本示例中名为 "Naive Bayes"）的 Python 代码作为输入传递给在评分过程中调用该模型的另一个存储过程。 此练习只使用一个模型，但您可以想像到计分任务中的模型参数化如何使该脚本更有用。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
