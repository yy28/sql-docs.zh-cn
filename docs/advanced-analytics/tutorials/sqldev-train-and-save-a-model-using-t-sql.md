---
title: 第3课使用 R 和 T-sql 定型和保存模型
description: 本教程演示如何使用 SQL Server 存储过程和 T-sql 函数对 R 模型进行定型、序列化和保存。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f23f4c350855b71a3633587bb3c092988fe89fef
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715337"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 课：使用 T-sql 定型和保存模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在本课程中, 您将学习如何使用 R 对机器学习模型进行训练。您将使用您在上一课中创建的数据功能来训练模型, 然后将训练的模型保存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中。 在这种情况下, R 包已随一起[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安装, 因此可以从 SQL 完成所有操作。

## <a name="create-the-stored-procedure"></a>创建存储过程

从 T-sql 调用 R 时, 可以使用系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但对于经常重复执行的进程 (如重新训练模型), 将对 sp_execute_exernal_script 的调用封装在另一个存储过程中会更容易。

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中, 打开一个新的**查询**窗口。

2. 运行以下语句以创建存储过程**RxTrainLogitModel**。 此存储过程定义输入数据并使用 RevoScaleR 中的**rxLogit**创建逻辑回归模型。

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - 为了确保某些数据已停留在测试模型上, 会从出租车数据表中随机选择 70% 的数据用于定型。

    - SELECT 查询使用自定义标量函数 *fnCalculateDistance* 计算上车与下车位置之间的直接距离。 查询的结果存储在默认 R 输入变量`InputDataset`中。
  
    - R 脚本会调用**rxLogit**函数, 该函数是[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中包含的增强的 R 函数之一, 用于创建逻辑回归模型。
  
        二进制变量 _tipped_ 用作标签或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
  
    - 被训练的模型 (保存在 R 变量`logitObj`中) 会进行序列化并作为输出参数返回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>使用存储过程训练和部署 R 模型

由于存储过程已包含输入数据的定义, 因此不需要提供输入查询。

1. 若要训练和部署 R 模型, 请调用存储过程并将其插入到数据库表_nyc_taxi_models_中, 以便可以将其用于将来的预测:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 查看**消息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , 查找将传送到 R 的**stdout**流的消息, 如下所示: 

    "来自外部脚本的 STDOUT 消息:读取的行数:1193025, 处理的总行数:1193025, 总区块时间:0.093 秒 "

    你可能还会看到特定于单个函数的消息`rxLogit`, 并显示作为模型创建的一部分生成的变量和测试指标。

3.  完成语句后, 打开表*nyc_taxi_models*。 处理数据并对模型进行调整可能需要一段时间。

    您可以看到, 添加了一个新行, 其中包含列_模型_中的序列化模型以及列_名称_中的模型名称**RxTrainLogit_model** 。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一步中, 您将使用训练的模型生成预测。

## <a name="next-lesson"></a>下一课

[第 4 课：在存储过程中使用 R 模型预测潜在结果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一课

[第 2 课：使用 R 和 T-sql 函数创建数据功能](..//tutorials/sqldev-create-data-features-using-t-sql.md)

