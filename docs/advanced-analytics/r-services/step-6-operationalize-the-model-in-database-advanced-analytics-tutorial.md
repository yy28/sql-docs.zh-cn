---
title: "步骤 6：操作模型（数据库中的高级分析教程） | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 步骤 6：操作模型（数据库中的高级分析教程）
在此步骤中，你将学习使用存储过程操作模型。 此存储过程可由其他应用程序直接调用，以就新的观测进行预测。  
  
在此步骤中，你将学习从存储过程调用 R 模型的两种方法：  
  
-   **批量评分模式**：使用 SELECT 查询提供多行数据。 存储过程将返回与输入事例对应的观测表。  
  
-   **单个评分模式**：传递一组单独的参数值作为输出。  存储过程将返回单个行或值。  
  
首先，让我们看看一般情况下评分的工作原理。  
  
## 基本评分  
存储过程 _PredictTip_ 说明了在存储过程中包装预测调用的基本语法。  
  
```  
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
str(OutputDataSet)  
print(OutputDataSet)  
',  
                                  @input_data_1 = @inquery,  
                                  @params = N'@model varbinary(max)',  
                                  @model = @lmodel2  
  WITH RESULT SETS ((Score float));  
  
END  
  
GO  
  
```  
  
-   SELECT 语句从数据库中获取序列化的模型，并将模型存储在 R 变量 `mod` 中以便使用 R 对其进行进一步处理。  
  
-   从 `@inquery` 中指定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询中获得要评分的新案例，它是存储过程的第一个参数。 读取查询数据时，行保存在默认数据帧 `InputDataSet` 中。 此数据帧将被传递给 R 中的 `rxPredict` 函数，该函数将生成评分。  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    由于数据帧可以包含单个行，你可以使用相同的代码来进行批量或单个评分。  
  
-   `rxPredict` 函数返回的值是 **float**，它表示给小费（任意数量）的概率。  
  
## 使用 SELECT 查询进行批量评分  
现在让我们看看批量评分的工作原理。  
  
1.  我们先获取要处理的较小输入数据集。  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    此查询创建了“排名前 10”的行程列表，其中需要预测乘客计数和其他功能。  
  
 **结果**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
你将使用此查询作为存储过程 _PredictTipBatchMode_ 的输入，它作为下载的一部分提供。  
  
2.  首先，花点时间查看 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中存储过程 _PredictTipBatchMode_ 的代码。  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
    AS  
    BEGIN  
  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
                                      @input_data_1 = @inquery,  
                                      @params = N'@model varbinary(max)',  
                                      @model = @lmodel2  
      WITH RESULT SETS ((Score float));  
  
    END  
    ```  
  
3.  若要创建预测，需要在变量中提供查询文本并使用与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 相似的语句将其作为参数传递给存储过程。  
  
    ```  
    -- Specify input query  
  
    DECLARE @query_string nvarchar(max)  
    SET @query_string='  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  存储过程将返回一系列值，表示对每个“排名前 10 的行程”的预测。 回头看输入值，所有“排名前 10 的行程”都是行程距离相对较短的单乘客行程。 根据数据来看，司机很有可能不会在这类行程中获得小费。  
  
    你可能还会返回该预测的概率评分（而不是返回有小费/无小费的结果），然后将一个 WHERE 子句应用到_分数_列的值以使用如 0.5 或 0.7 之类的阈值将评分分类为“可能会给小费”或“不可能给小费”。 此步骤不包含在存储过程中，但很容易执行。  
  
## 对单独的行进行评分  
有时你想要从应用程序以单一值传递并基于这些值获取单个结果。 例如，你可以设置 Excel 工作表、Web 应用程序或 Reporting Services 报表，以调用存储过程和提供用户键入或选择的输入信息。  
  
在本部分中，你将了解如何使用存储过程创建单个预测。  
  
1.  花点时间查看存储过程 _PredictTipSingleMode_ 的代码，它作为下载的一部分提供。  
  
    ```  
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0  
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
    @model = @lmodel2,  
    @passenger_count =@passenger_count ,  
    @trip_distance=@trip_distance,  
    @trip_time_in_secs=@trip_time_in_secs,    
    @pickup_latitude=@pickup_latitude,  
    @pickup_longitude=@pickup_longitude,  
    @dropoff_latitude=@dropoff_latitude,  
    @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
  
    END  
  
    ```  
  
    -   此存储过程将多个单一值作为输入，例如乘客计数、行程距离等。  
  
        如果从外部应用程序调用存储过程，请确保数据满足 R 模型的要求。 这可能包括确保输入的数据可以被转换为 R 数据类型或验证数据类型和数据长度。 有关详细信息，请参阅[使用 R 数据类型](https://msdn.microsoft.com/library/mt590948.aspx)。  
  
    -   存储过程根据存储的 R 模型创建评分。  
  
2.  通过手动提供值来进行试用。  
  
    打开一个新的“查询”窗口，调用存储过程，为每个特征列键入参数。  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    这些值针对这些特征列，按顺序为：  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  结果表明从排名前 10 的行程中获得小费的概率非常低，所有这些行程都是距离相对较短的单乘客行程。  
  
## 结论  
在本教程中，你已了解如何使用存储过程中嵌入的 R 代码。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成使其更易于部署 R 模型以进行预测，将模型再定型合并为企业数据工作流的一部分也变得更加容易。  
  
  
## 上一步  
[步骤 4：使用 T-SQL 创建数据功能](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 另请参阅  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
