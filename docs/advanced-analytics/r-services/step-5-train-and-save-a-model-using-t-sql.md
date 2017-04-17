---
title: "步骤 5：使用 T-SQL 训练和保存模型 | Microsoft Docs"
ms.custom: 
ms.date: 04/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1c2786aa72bd33fd9ea046ae5a5075e1d49e50b8
ms.lasthandoff: 04/11/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>步骤 5：使用 T-SQL 定型和保存模型
在此步骤中，你将学习如何使用 R 定型机器学习模型。R 包已随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安装，因此你可以从存储过程调用算法。 你将使用刚创建的数据特征定型模型，然后将已定型模型保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
## <a name="building-an-r-model-using-stored-procedures"></a>使用存储过程生成 R 模型  
对随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安装的 R 运行时进行的所有调用都使用系统存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来执行。 但是，如果需要重新定型模型，则在其他存储过程中封装对 sp_execute_exernal_script 进行的调用可能会更加方便。  
  
在此部分中，你将创建一个存储过程，它可以用于通过刚准备好的数据来生成模型。 此存储过程定义输入数据，并使用 R 包创建逻辑回归模型。  
  
#### <a name="to-create-the-stored-procedure"></a>创建存储过程  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开一个新查询窗口并运行以下语句以创建存储过程 _TrainTipPredictionModel_。  
  
    请注意，因为存储过程已包含输入数据的定义，所以无需提供输入查询。  
  
    ```  
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
  
    此存储过程在模型定型过程中执行这些活动：  
  
    -   为了确保留下一些数据以测试模型，70% 的数据是从出租车数据表中随机选择的。  
  
    -   SELECT 查询使用自定义标量函数 _fnCalculateDistance_ 计算上车与下车位置之间的直接距离。  查询的结果存储在默认 R 输入变量 `InputDataset`中。  
  
    -   R 脚本会调用 `rxLogit` 函数（这是 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 附带的一个增强 R 函数）以创建逻辑回归模型。  
  
        二进制变量 _tipped_ 用作标签或结果列，模型使用以下这些特征列进行调整：_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。  
  
    -   已定型模型（保存在 R 变量 `logitObj` 中）会进行序列化，并置于数据帧中以便输出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 该输出会插入数据库表 _nyc_taxi_models_中，以便你可以将它用于将来的预测。  
  
2.  运行该语句以创建存储过程。  
  
#### <a name="to-create-the-r-model-using-the-stored-procedure"></a>使用存储过程创建 R 模型  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行此语句。  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    数据处理和模型调整可能需要一些时间。 通过管道传递到 R 的 **stdout** 流的消息会显示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的“消息”窗口中。 例如：  
  
  
*STDOUT message(s) from external script: Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds*       
  
会读取并处理连续的数据块。 你可能还会看到特定于单个函数 `rxLogit` 的消息（指示变量和测试度量值）。  
  
2.  打开表 nyc_taxi_models。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。  
  
  
  
*model*  
*0x580A00000002000302020....*  
  
在下一步中，你将使用已定型模型来创建预测。  
  
## <a name="next-step"></a>下一步  
[步骤 6：操作模型](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## <a name="previous-step"></a>上一步  
[步骤 4：使用 T-SQL 创建数据功能](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  


