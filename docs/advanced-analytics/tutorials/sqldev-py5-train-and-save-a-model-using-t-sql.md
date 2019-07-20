---
title: 使用 T-sql 定型和保存 Python 模型
description: Python 教程介绍了如何使用 Transact-sql 在 SQL Server 上定型和保存模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: dbe5bcb39ddbcc2b4968beccb9363a92cf6e8817
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345871"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>使用 T-sql 定型和保存 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是[针对 SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)教程的一部分。 

在此步骤中, 你将了解如何使用 Python 包**scikit-learn**和**revoscalepy**训练机器学习模型。 这些 Python 库已安装了 SQL Server 机器学习服务。

您可以加载模块并调用必要的函数以使用 SQL Server 存储过程创建和训练模型。 模型需要在前面的课程中设计的数据功能。 最后, 将训练的模型保存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>将示例数据拆分为定型集和测试集

1. 创建名为**PyTrainTestSplit**的存储过程, 将 nyctaxi_sample 表中的数据分为两部分: nyctaxi_sample_training 和 nyctaxi_sample_testing。 

    应该已经为你创建了此存储过程, 但可以运行以下代码来创建它:

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 若要使用自定义拆分来划分数据, 请运行存储过程, 并键入一个整数, 该整数表示分配给定型集的数据的百分比。 例如, 下面的语句会将 60% 的数据分配到定型集。

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>构建逻辑回归模型

准备好数据后, 可以使用它来训练模型。 为此, 请调用运行某些 Python 代码的存储过程, 并将其作为输入定型数据表。 在本教程中, 将创建两个模型, 两个都是二元分类模型:

+ 存储过程**PyTrainScikit**使用**scikit-learn**包创建 tip 预测模型。
+ 存储过程**TrainTipPredictionModelRxPy**使用**revoscalepy**包创建 tip 预测模型。

每个存储过程都使用您提供的输入数据来创建和训练逻辑回归模型。 所有 Python 代码都包装在系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中。

为了更轻松地对新数据重新训练模型, 你可以将对 sp_execute_exernal_script 的调用包装在另一个存储过程中, 并以参数的形式传递新的定型数据。 本部分将引导你完成该过程。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中, 打开一个新的**查询**窗口, 然后运行以下语句来创建存储过程**PyTrainScikit**。  存储过程包含输入数据的定义, 因此不需要提供输入查询。

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
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

2. 运行以下 SQL 语句, 将训练的模型插入到表 nyc\_taxi_models 中。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    处理数据并对模型进行调整可能需要几分钟的时间。 将输送到 Python 的**stdout**流的消息显示在的 "**消息**" 窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 例如：

    *来自外部脚本的 STDOUT 消息:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 打开表*nyc\_taxi_models*。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

此存储过程使用新的**revoscalepy**包, 这是 Python 的新包。 它包含类似于为 R 语言的**RevoScaleR**包提供的对象、转换和算法。 

通过使用**revoscalepy**, 可以创建远程计算上下文, 在计算上下文之间移动数据, 转换数据, 以及使用常见算法 (如逻辑和线性回归、决策树等) 训练预测模型。 有关详细信息, 请参阅 SQL Server 和[revoscalepy 函数参考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)[中的 revoscalepy 模块](../python/ref-py-revoscalepy.md)。

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中, 打开一个新的**查询**窗口, 然后运行以下语句来创建存储过程_TrainTipPredictionModelRxPy_。  由于存储过程已包含输入数据的定义, 因此不需要提供输入查询。

    ```sql
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

    此存储过程在模型训练过程中执行以下步骤:

    - SELECT 查询将应用自定义标量函数_fnCalculateDistance_来计算拾取位置与下拉位置之间的直接距离。 查询的结果存储在默认的 Python 输入变量`InputDataset`中。
    - 二进制变量_附属_项用作*标签*列或结果列, 模型适合使用以下功能列: _passenger_count_、 _trip_distance_、 _trip_time_in_secs_和_direct_distance_。
    - 训练的模型被序列化并存储在 Python 变量`logitObj`中。 通过添加 T-sql 关键字输出, 你可以将变量添加为存储过程的输出。 在下一步中, 该变量用于将模型的二进制代码插入到数据库表_nyc_taxi_models_中。 利用此机制, 可以轻松地存储和重新使用模型。

2. 按如下所示运行存储过程, 将训练的**revoscalepy**模型插入表*nyc_taxi_models*。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    处理数据并对模型进行调整可能需要一段时间。 将输送到 Python 的**stdout**流的消息显示在的 "**消息**" 窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 例如：

    *来自外部脚本的 STDOUT 消息:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 打开表 nyc_taxi_models  。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *revoscalepy_model* *0x8003637265766F7363616c....*

在下一步中, 您将使用训练的模型来创建预测。

## <a name="next-step"></a>下一步

[使用存储过程中嵌入的 Python 运行预测](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一步

[使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)
