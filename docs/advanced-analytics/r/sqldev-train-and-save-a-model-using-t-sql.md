---
title: "第 5 课： 训练和保存模型使用 T-SQL |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41176650541844b835505a6805f5437b2ea061b1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>第 5 课： 训练和保存模型使用 T-SQL

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

在本课程中，你将学习如何使用。 来训练机器学习模型你将使用刚创建的数据功能训练该模型，然后保存训练的模型中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 在这种情况下，与已安装 R 包[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此所有内容可以从 SQL。

## <a name="create-the-stored-procedure"></a>创建存储的过程

当从 T-SQL 调用 R，使用系统存储过程中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但是，对于你重复通常情况下，例如重新训练模型的进程是更轻松地封装到调用`sp_execute_exernal_script`另一个存储过程。

1.  首先，创建包含用于生成提示预测模型的 R 代码的存储的过程。 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口并运行以下语句以创建存储的过程_TrainTipPredictionModel_。 此存储过程定义输入数据，并使用 R 包创建逻辑回归模型。

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - 但是，若要确保某些数据留下来测试模型，70%的数据是随机选择从 taxi 数据表。
    
    - SELECT 查询使用自定义标量函数 _fnCalculateDistance_ 计算上车与下车位置之间的直接距离。  查询的结果存储在默认 R 输入变量 `InputDataset`中。
  
    - R 脚本调用`rxLogit`函数，这是一个增强的 R 函数附带[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以创建逻辑回归模型。
  
        二进制变量 _tipped_ 用作标签或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
  
    -   已定型模型（保存在 R 变量 `logitObj` 中）会进行序列化，并置于数据帧中以便输出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 该输出会插入数据库表 _nyc_taxi_models_中，以便你可以将它用于将来的预测。
  
2.  如果它尚不存在，请运行语句以创建该存储的过程。

## <a name="generate-the-r-model-using-the-stored-procedure"></a>生成使用存储的过程的 R 模型

由于存储的过程已包含的输入数据的定义，不需要提供的输入的查询。

1. 若要生成 R 模型，请调用不带任何其他参数的存储的过程：

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. 监视**消息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的消息将传送到 R 的**stdout**流，如此 messaage: 

    "来自外部脚本的 STDOUT 消息： 行读取： 1193025，总行处理： 1193025，总区块时间： 0.093 （秒)"

    你还可能看到特定于单个函数，消息`rxLogit`、 显示变量和测试模型创建过程中生成的度量值。

3.  在完成该语句后，打开表*nyc_taxi_models*。 处理的数据和拟合模型可能需要一些时间。

    可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    ```
    model
    ------
    0x580A00000002000302020....
    ```

在下一步中，你将使用已定型模型来创建预测。

## <a name="next-lesson"></a>下一课

[第 6 课： 实施该模型](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一课

[第 4 课： 创建使用 T-SQL 的数据功能](..//tutorials/sqldev-create-data-features-using-t-sql.md)

