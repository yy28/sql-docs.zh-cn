---
title: "步骤 5：使用 T-SQL 训练和保存模型 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>步骤 5： 训练和保存模型使用 T-SQL

在此步骤中，你学习如何使用 Python 包机器学习模型进行定型**scikit-了解**和**revoscalepy**。 这些 Python 库已经安装了与 SQL Server 计算机学习 Services，以便你可以加载模块并调用存储过程中从所需的函数。 你将使用刚创建的数据特征定型模型，然后将已定型模型保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>将示例数据拆分为定型集和测试集

1. 运行下面的 T-SQL 命令，以创建将划分 nyctaxi 中的数据的存储的过程\_分为两部分的示例表： nyctaxi\_示例\_培训和 nyctaxi\_示例\_测试。

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

2. 运行存储的过程，并键入一个整数，表示到训练集的分配的数据的百分比。 例如，以下语句将分配到训练集的数据的 60%。 定型集和测试数据存储在两个单独的表。

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>使用生成一个逻辑回归模型 scikit-了解

在本部分中，你将创建可以用于训练模型使用只是准备训练数据的存储的过程。 此存储的过程定义的输入的数据，并使用**scikit-了解**函数逻辑回归模型进行定型。 调用通过使用系统存储过程中，与 SQL Server 安装的 Python 运行[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

若要更加轻松地重新训练模型，可以到 sp_execute_exernal_script 的调用包装在另一个存储过程中，并在新的定型数据作为参数传递。 本部分将引导你完成该过程。

1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口并运行以下语句以创建存储的过程_TrainTipPredictionModelSciKitPy_。  请注意，存储的过程将包含的输入数据的定义，因此无需提供的输入的查询。

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
      import pandas
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

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>生成逻辑模型使用_revoscalepy_包

现在，创建不同的存储的过程中使用新**revoscalepy**定型逻辑回归模型的包。 **Revoscalepy**打包 Python 包含对象、 转换和算法类似于所提供的 R 语言**RevoScaleR**包。 使用此库中，你可以创建计算上下文，移动之间的数据计算上下文、 转换数据，和使用受欢迎的算法，如逻辑和线性回归、 决策树，以及更多的预测模型定型。 有关详细信息，请参阅[revoscalepy 是什么？](../python/what-is-revoscalepy.md)

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口并运行以下语句以创建存储的过程_TrainTipPredictionModelRxPy_。  此模型也使用只是准备定型数据。 由于存储的过程已包含的输入数据的定义，不需要提供的输入的查询。

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
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - 逻辑回归使用训练模型 revoscalepy 包上 nyctaxi\_示例\_定型数据。
    - SELECT 查询使用自定义标量函数 _fnCalculateDistance_ 计算上车与下车位置之间的直接距离。 查询的结果将存储在默认 Python 输入变量中， `InputDataset`。
    - Python 脚本调用 revoscalepy LogisticRegression 函数时，它又包括在[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以创建逻辑回归模型。
    - 二进制变量 _tipped_ 用作标签或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
    - 训练的模型包含在 Python 变量`logitObj`、 序列化并作为输出参数将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 输出插入到数据库表_nyc_taxi_models_，以及其名称，作为新行的名称，以便可以检索并将其用于将来的预测。

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

[步骤 6： 实施该模型](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一步

[步骤 4： 创建使用 T-SQL 的数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

