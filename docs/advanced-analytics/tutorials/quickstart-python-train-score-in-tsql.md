---
title: 快速入门 Python 模型训练和预测使用的存储过程的 SQL Server 机器学习
description: 在 SQL Server 存储过程来创建、 定型和使用经典的鸢尾花数据集使用 Python 模型中嵌入 Python 代码。 将训练的模型保存到 SQL Server，然后使用它来生成预测的结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e8bacc383eba1148c1b357c344bc483e824df99b
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046767"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>快速入门：创建、 定型和 SQL Server 中使用存储过程中使用 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此快速入门中使用 Python，您将创建并执行两个存储的过程。 第一个使用经典鸢尾花卉数据集，并生成一个朴素贝叶斯模型来预测鸢尾花物种花卉特征。 第二个过程是进行评分。 它将调用输出一组预测的第一个步骤中生成的模型。 通过将代码放置在存储过程中，操作是包含、 可重用的和可调用其他存储的过程和客户端应用程序。 

通过完成本快速入门中，您将了解：

> [!div class="checklist"]
> * 如何在存储过程中嵌入 Python 代码
> * 如何将通过输入在代码的输入传递存储过程
> * 如何使用存储的过程来操作模型

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 Python](quickstart-python-verify.md)、 提供的信息和链接设置为本快速入门所需的 Python 环境。

在此练习中使用的示例数据是[ **irissql** ](demo-data-iris-in-sql.md)数据库。

## <a name="create-a-stored-procedure-that-generates-models"></a>创建一个存储的过程，生成模型

SQL Server 开发中的常见模式是组织到不同的存储过程的可编程操作。 在此步骤中，将创建生成的模型的预测结果的存储的过程。 

1. 打开 Management Studio 中新的查询窗口连接到**irissql**数据库。 

    ```sql
    USE irissql
    GO
    ```

2. 以下代码以创建新的存储的过程中的复制。 

   执行时，此过程将调用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)启动 Python 会话。 
   
   输入所需的 Python 代码将此存储过程传递作为输入参数。 输出将为训练的模型基于 Python **scikit-了解**适用于机器学习算法库。 

   此代码使用[ **pickle** ](https://docs.python.org/2/library/pickle.html)要序列化模型。 将使用从 0 到 4 列中的数据训练模型**iris_data**表。 
   
   您在该过程的第二部分中看到的参数清楚地讲述数据输入和模型输出。 尽可能多地，你想要有明确的输入的存储过程中运行的 Python 代码，并输出映射到存储的过程输入和输出在运行时中传递。 

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

3. 验证存储的过程存在。 

   如果在上一步中的 T-SQL 脚本运行正常，一个新的存储过程调用**generate_iris_model**被创建并添加到**irissql**数据库。 可以在 Management Studio 中找到存储的过程**对象资源管理器**下**可编程性**。

## <a name="execute-the-procedure-to-create-and-train-models"></a>执行该过程以创建并定型模型

在此步骤中，执行该过程以运行嵌入的代码中，创建作为输出模型训练和序列化的模型。 序列化为字节流和存储在数据库表中的 varbinary （max） 列中以供重复使用 SQL Server 中存储的模型。 一旦创建、 训练、 序列化，并保存到数据库模型，它可以调用其他过程或通过[预测 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)评分工作负荷中的函数。

1. 复制下面的代码执行该过程。 用于执行存储的过程的特定语句是`EXEC`第五个行上。

   此特定脚本中删除现有的同名 ("Naive Bayes") 以容纳所通过重新运行相同的过程创建新的模型。 而不执行模型删除出错时指出该对象已存在。 模型存储在名为的表**iris_models**，在创建时预配**irissql**数据库。

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 验证是否已插入该模型是另一种方法来返回模型的列表

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **结果**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>创建和执行用于生成预测的存储的过程

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

## <a name="conclusion"></a>结束语

在此练习中，您学习了如何创建专用于不同的任务，其中每个存储的过程使用系统存储过程的存储的过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)启动 Python 进程。 到 Python 进程的输入作为参数传递给 sp_execute_external 脚本。 Python 脚本本身和 SQL Server 数据库中的数据变量作为输入传递。

通常情况下，您应仅计划通过 SSMS 使用经过精心设计的 Python 代码或返回基于行的输出的简单 Python 代码。 作为一种工具，SSMS 支持 T-SQL 之类的查询语言，并返回平展行集。 如果你的代码生成类似于散点图或柱状图 visual 输出，则需要可以呈现图像的工具或最终用户应用程序。

对于某些 Python 开发人员习惯于编写一价全包脚本处理一系列操作，将任务组织成单独的过程看起来不必要。 但定型和计分具有不同的用例。 分隔它们，可以将每个任务放置在不同的计划和操作的作用域权限。

同样，您还可以利用资源功能的 SQL Server，如并行处理，资源调控功能，或通过编写脚本以使用中的算法[revoscalepy](../python/ref-py-revoscalepy.md)或[microsoftml](../python/ref-py-microsoftml.md) ，支持流式处理和并行执行。 通过将训练和评分，可以面向特定的工作负荷的优化。

最后一个优点是可以使用参数修改进程。 在此练习中，在创建模型 （在此示例中，名为"Naive Bayes"） 的 Python 代码作为第二个存储过程在评分过程中调用模型的输入传递。 本练习中仅使用一个模型，但您可以想象如何参数化的模型中的评分任务会使该脚本更有用。

## <a name="next-steps"></a>后续步骤

如果你是 SQL 开发人员接触 Python，可以移动到远程 SQL Server 实例执行本地会话中的查看用于本地，Python 代码的工具和步骤。

> [!div class="nextstepaction"]
> [设置 Python 客户端工作站](../python/setup-python-client-tools-sql.md)。

