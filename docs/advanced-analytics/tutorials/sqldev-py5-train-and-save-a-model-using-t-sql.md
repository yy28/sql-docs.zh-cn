---
title: Python + T-SQL：定型模型
description: 演示如何使用 Transact-SQL 在 SQL Server 上定型和保存模型的 Python 教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 87194c1a77964f0e5aef3d0fae008d14cbfb8eb2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "74901807"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>使用 T-SQL 定型和保存 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文属于[适用于 SQL 开发者的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)这一教程。 

在此步骤中，你可了解如何使用 Python 包 scikit-learn 和 revoscalepy 来定型机器学习模型   。 这些 Python 库已随 SQL Server 机器学习服务安装。

加载模块并调用必要的函数，以使用 SQL Server 存储过程创建和定型模型。 该模型需要在前面的课程中设计的数据功能。 最后，将定型后的模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>将示例数据拆分为定型集和测试集

1. 创建名为 PyTrainTestSplit 的存储过程，以将 nyctaxi_sample 表中的数据划分为两部分：nyctaxi_sample_training 和 nyctaxi_sample_testing  。 

    此时应该已创建此存储过程，但你也可运行以下代码来创建该过程：

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

2. 要使用自定义拆分来划分数据，请运行存储过程，并键入一个整数，该整数表示分配给定型集的数据的百分比。 例如，以下语句会将 60% 的数据分配给定型集。

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>构建逻辑回归模型

数据准备就绪后，可以使用它来定型模型。 为此，可以调用运行某些 Python 代码的存储过程，并将其作为定型数据表的输入。 在本教程中，你将创建两个模型，并且这两个模型都是二元分类模型：

+ 存储过程 PyTrainScikit 使用 scikit-learn 包创建小费预测模型   。
+ 存储过程 TrainTipPredictionModelRxPy 使用 revoscalepy 包创建小费预测模型   。

每个存储过程都使用你提供的输入数据来创建和定型逻辑回归模型。 所有 Python 代码都包装在系统存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中。

为了更轻松地基于新数据重新定型模型，可以将对 sp_execute_external_script 的调用包装在另一存储过程中，并将新的定型数据作为参数传入。 本部分将引导你完成该过程。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，打开一个新“查询”窗口并运行以下语句以创建存储过程 PyTrainScikit   。  因为存储过程包含输入数据的定义，所以无需提供输入查询。

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

2. 运行以下 SQL 语句，将定型后的模型插入到表 nyc\_taxi_models 中。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    数据处理和模型调整可能需要几分钟时间。 通过管道传递到 Python 的 stdout 流的消息会显示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的“消息”窗口中   。 例如：

    来自外部脚本的 STDOUT 消息: 
  C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy  

3. 打开表 nyc\_taxi_models  。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

此存储过程使用新的 revoscalepy 包，此包为 Python 的新包  。 它所包含的对象、转换和算法与为 R 语言的 RevoScaleR 包提供的对象、转换和算法类似  。 

通过使用 revoscalepy，可以创建远程计算上下文、在计算上下文之间移动数据、转换数据并使用常见算法（如逻辑和线性回归、决策树等）定型预测模型  。 有关详细信息，请参阅 [SQL Server 中的 revoscalepy 模块](../python/ref-py-revoscalepy.md)和 [revoscalepy 函数参考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)。

1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，打开新的“查询”窗口并运行以下语句以创建存储过程 TrainTipPredictionModelRxPy   。  因为存储过程已包含输入数据的定义，所以无需提供输入查询。

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

    此存储过程在模型定型过程中执行以下步骤：

    - SELECT 查询应用自定义标量函数 fnCalculateDistance 计算上车与下车位置之间的直接距离  。 查询的结果存储在默认 Python 输入变量 `InputDataset` 中。
    - 二进制变量 tipped 用作标签或结果列，模型使用以下这些特征列进行调整：passenger_count、trip_distance、trip_time_in_secs 和 direct_distance       。
    - 定型后的模型将进行序列化并存储在 Python 变量 `logitObj` 中。 通过添加 T-SQL 关键字 OUTPUT，可以将变量添加为存储过程的输出。 在下一步中，该变量用于将模型的二进制代码插入到数据库表 nyc_taxi_models 中  。 借助此机制，可轻松存储和重新使用模型。

2. 按如下所示运行存储过程，将定型后的 revoscalepy 模型插入到表 nyc_taxi_models 中   。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    数据处理和模型调整可能需要一些时间。 通过管道传递到 Python 的 stdout 流的消息会显示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的“消息”窗口中   。 例如：

    来自外部脚本的 STDOUT 消息: 
  C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy  

3. 打开表 nyc_taxi_models  。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *revoscalepy_model* *0x8003637265766F7363616c....*

在下一步中，使用已定型模型来创建预测。

## <a name="next-step"></a>后续步骤

[使用存储过程中嵌入的 Python 来运行预测](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一步

[使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)
