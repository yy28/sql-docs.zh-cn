---
title: R + T-SQL 教程：定型模型
description: 教程演示如何使用 SQL Server 存储过程和 T-SQL 函数来定型、序列化和保存 R 模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115780"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 课：使用 T-SQL 定型和保存模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文属于有关如何在 SQL Server 中使用 R 的 SQL 开发者教程。

在本课程中，你可学习如何使用 R 定型机器学习模型。使用在上一课程中创建的数据特征来定型该模型，然后将定型后的模型保存到一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。 在本例中，R 包已随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安装，因此可通过 SQL 完成所有操作。

## <a name="create-the-stored-procedure"></a>创建存储过程

从 T-SQL 调用 R 时，可以使用系统存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但是，对于经常重复执行的过程（如重新定型模型），在其他存储过程中封装对 sp_execute_exernal_script 进行的调用则会更加方便。

1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，打开一个新的“查询”窗口  。

2. 运行以下语句，创建存储过程 RxTrainLogitModel  。 此存储过程定义输入数据，并使用 RevoScaleR 中的 rxLogit 创建逻辑回归模型  。

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

    - 为了确保留下一些数据以测试模型，70% 的数据是出于定型目的从出租车数据表中随机选择的。

    - SELECT 查询使用自定义标量函数 *fnCalculateDistance* 计算上车与下车位置之间的直接距离。 查询的结果存储在默认 R 输入变量 `InputDataset` 中。
  
    - R 脚本会调用 rxLogit 函数（这是 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 附带的一个增强 R 函数）以创建逻辑回归模型  。
  
        二进制变量 _tipped_ 用作标签  或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
  
    - 已定型模型（保存在 R 变量 `logitObj` 中）会进行序列化，并作为输出参数返回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>使用存储过程定型并部署 R 模型

因为存储过程已包含输入数据的定义，所以无需提供输入查询。

1. 要定型和部署 R 模型，请调用存储过程，并将其插入到数据库表 nyc_taxi_models 中，以便可以将其用于未来的预测  ：

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 查看 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的“消息”窗口，以查看通过管道传递到 R 的 stdout 流的消息，如下所示   ： 

    “来自外部脚本的 STDOUT 消息:读取的行数：1193025，已处理的总行数:1193025，总区块时间:0.093 秒”

    可能还会看到特定于单个函数 `rxLogit` 的消息（显示作为模型创建的一部分生成的变量和测试指标）。

3.  语句完成后，打开表 nyc_taxi_models  。 数据处理和模型调整可能需要一些时间。

    可以看到已添加了一个新行，该行在列 model 中包含序列化模型，在列 name 中包含模型名称 RxTrainLogit_model    。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一步中，使用已定型模型来生成预测。

## <a name="next-lesson"></a>下一课

[第 4 课：在存储过程中使用 R 模型预测潜在结果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一课

[第 2 课：使用 R 和 T-SQL 函数创建数据特征](..//tutorials/sqldev-create-data-features-using-t-sql.md)

