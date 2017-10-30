---
title: "步骤 5： 训练和保存使用 T-SQL 的 Python 模型 |Microsoft 文档"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 11fa031229d8bc08a9091c3fa6f85e81468d7379
ms.contentlocale: zh-cn
ms.lasthandoff: 10/18/2017

---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>步骤 5： 训练和保存 Python 模型使用 T-SQL

使用本教程，本文摘自[SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，你学习如何使用 Python 包机器学习模型进行定型**scikit-了解**和**revoscalepy**。 与 SQL Server 计算机学习 Services 已安装这些 Python 库。

你加载模块并调用所需的函数来创建并定型模型时使用 SQL Server 存储过程。 模型需要在之前的课程中工程处理的数据功能。 最后，保存到训练的模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。

> [!IMPORTANT]
> 发生了中的多项更改**revoscalepy**包，其中此教程所需的代码中的小更改。 请参阅[更改列表](sqldev-py6-operationalize-the-model.md#changes)在本教程末尾。 
> 
> 如果您在安装 Python 服务使用 SLq Server 2017 的预发布版本，我们建议你升级到最新版本。 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>将示例数据拆分为定型集和测试集

1. 你可以使用存储的过程**TrainTestSplit**来划分 nyctaxi 中的数据\_分为两部分的示例表： nyctaxi\_示例\_培训和 nyctaxi\_示例\_测试。 

    此存储的过程应已创建，但你可以运行下面的代码来创建它：

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 若要将使用自定义拆分数据，运行存储的过程，并键入一个整数，表示到训练集的分配的数据的百分比。 例如，以下语句将分配到训练集的数据的 60%。

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>生成一个逻辑回归模型

数据已准备好后，你可以使用它来训练某个模型。 执行此操作通过调用存储过程来运行一些 Python 代码，采用作为输入的训练数据的表。 对于本教程，你可以创建两个模型，这两个二元分类模型：

+ 存储的过程**TrainTipPredictionModelRxPy**创建提示预测模型使用**revoscalepy**包。
+ 存储的过程**TrainTipPredictionModelSciKitPy**创建提示预测模型使用**scikit-了解**包。

每个存储的过程使用输入的数据您提供用来创建并定型逻辑回归模型。 所有的 Python 代码包装在系统存储过程中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

若要更加轻松地重新训练上新数据的模型，请到 sp_execute_exernal_script 的调用包装在另一个存储过程中，并在新的定型数据作为参数传递。 本部分将引导你完成该过程。

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口并运行以下语句以创建存储的过程_TrainTipPredictionModelSciKitPy_。  存储的过程包含的输入数据的定义，因此无需提供的输入的查询。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
      EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
      import numpy
      import pickle
      from sklearn.linear_model import LogisticRegression
      
      ##Create SciKit-Learn logistic regression model
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      SKLalgo = LogisticRegression()
      logitObj = SKLalgo.fit(X, y)
      
      ##Serialize model
      trained_model = pickle.dumps(logitObj)
      ',
      @input_data_1 = N'
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_training
      ',
      @input_data_1_name = N'InputDataSet',
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT;
      ;
    END;
    GO
    ```

2. 运行以下 SQL 语句插入到训练的模型表 nyc\_taxi_models。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    处理的数据和拟合模型可能需要几分钟。 消息将传送到 Python 的**stdout**流将显示在**消息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *来自外部脚本的 STDOUT 消息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 打开表*nyc\_taxi_models*。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *linear_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

此存储的过程使用新**revoscalepy**包，这是新 Python 包。 它包含对象、 转换和算法类似于所提供的 R 语言**RevoScaleR**包。 

通过使用**revoscalepy**，您可以创建远程计算上下文、 之间移动数据计算上下文、 转换数据和训练预测模型使用常用的算法，如逻辑和线性回归，决策树和更多。 有关详细信息，请参阅[revoscalepy 是什么？](../python/what-is-revoscalepy.md)

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口并运行以下语句以创建存储的过程_TrainTipPredictionModelRxPy_。  由于存储的过程已包含的输入数据的定义，不需要提供的输入的查询。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    此存储的过程作为模型定型的一部分执行以下步骤：

    - 将自定义的标量函数的 SELECT 查询应用_fnCalculateDistance_以计算提取和放置位置之间的直接距离。 查询的结果将存储在默认 Python 输入变量中， `InputDataset`。
    - 二进制变量_附属式_用作*标签*或结果列和模型适合使用这些功能列： _passenger_count_， _trip_距离_， _trip_time_in_secs_，和_direct_distance_。
    - 序列化训练的模型并将其存储在 Python 变量`logitObj`。 通过添加 T-SQL 关键字输出，可以添加变量，作为存储过程的输出。 在下一步的步骤中，该变量用于将模型的二进制代码插入到数据库表_nyc_taxi_models_。 此机制，可轻松地存储和重复使用的模型。

2. 运行存储的过程，如下所示，若要插入训练**revoscalepy**模型到表 _nyc\_taxi\_模型。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    处理的数据和拟合模型可能需要一些时间。 消息将传送到 Python 的**stdout**流将显示在**消息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *来自外部脚本的 STDOUT 消息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 打开表 nyc_taxi_models。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *rx_model* *0x8003637265766F7363616c...*

在下一步的步骤中，你可以使用训练的模型创建预测。

## <a name="next-step"></a>下一步

[步骤 6： 具有可操作性 Python 模型时使用 SQL Server](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一步

[步骤 4：使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

