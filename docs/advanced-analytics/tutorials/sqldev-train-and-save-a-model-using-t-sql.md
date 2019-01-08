---
title: 课程 3 的训练和保存使用 R 和 T-SQL 的 SQL Server 机器学习模型
description: 教程显示如何训练、 序列化，和保存 R 模型使用的 SQL Server 存储过程和 T-SQL 的函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f3abe58aac4d5920e64337f63a40dc8f87fb12d9
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645106"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 课：训练和保存使用 T-SQL 的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在本课程中，您将学习如何使用 R 定型机器学习模型将训练该模型使用在上一课中创建的数据功能，然后将保存已训练的模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 在这种情况下，使用已安装 R 包[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此可以从 SQL 完成所有内容。

## <a name="create-the-stored-procedure"></a>创建存储的过程

在从 T-SQL 调用 R，使用系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但是，您通常情况下，如重新训练模型，重复的进程是更轻松地封装对 sp_execute_exernal_script 中另一个存储过程的调用。

1. 在中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口。

2. 运行以下语句以创建存储的过程**RxTrainLogitModel**。 此存储的过程定义输入的数据，并使用**rxLogit**从 RevoScaleR 创建逻辑回归模型。

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

    - 若要确保某些数据留下来测试模型，70%的数据是随机选择的培训目的出租车数据表中。

    - SELECT 查询使用自定义标量函数 *fnCalculateDistance* 计算上车与下车位置之间的直接距离。 查询的结果存储在默认 R 输入变量， `InputDataset`。
  
    - R 脚本会调用**rxLogit**函数，这是增强型 R 函数之一附带[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以创建逻辑回归模型。
  
        二进制变量 _tipped_ 用作标签或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
  
    - 在 R 变量中保存的定型的模型`logitObj`、 序列化并作为输出参数返回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>训练和部署 R 模型使用存储的过程

由于存储的过程已包含输入数据的定义，因此不需要提供输入的查询。

1. 若要训练和部署 R 模型，调用存储的过程，并将其插入到数据库表_nyc_taxi_models_，以便可以使用它用于将来的预测：

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 观看**消息**窗口中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的消息将传送到 R 的**stdout**流，方式与此消息类似： 

    "来自外部脚本的 STDOUT 消息：读取的行：1193025，处理的总行数：1193025，区块总时间：0.093 秒数"

    您可能还会看到特定于单个函数，消息`rxLogit`、 显示变量和测试模型创建的一部分生成的度量值。

3.  完成该语句后，打开表*nyc_taxi_models*。 数据处理和模型调整可能需要一段时间。

    可以看到已添加一个新行，其中包含的列中的序列化的模型_模型_和模型名称**RxTrainLogit_model**列中_名称_。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一步将使用经过训练的模型生成预测。

## <a name="next-lesson"></a>下一课

[第 4 课：预测潜在的存储过程中使用 R 模型的结果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一课

[第 2 课：使用 R 和 T-SQL 函数创建数据功能](..//tutorials/sqldev-create-data-features-using-t-sql.md)

