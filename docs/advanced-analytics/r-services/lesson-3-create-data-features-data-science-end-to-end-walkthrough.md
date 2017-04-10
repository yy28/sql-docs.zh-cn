---
title: "第 3 课：创建数据功能（数据科学端到端演练） | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 第 3 课：创建数据功能（数据科学端到端演练）
数据工程是机器学习的另一个重要组成部分。 通常需要先转换数据，然后才能使用数据进行预测建模。 如果数据不具有所需的功能，可根据现有值进行创建。  
  
对于此建模任务，想要以英里表示的上车和下车位置之间的距离，而不是使用这两个位置的原始纬度和经度值。 若要创建此功能，需要使用 [haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)计算两个点之间的直线距离。  
将比较用于通过数据创建功能的两个不同方法：  
  
-   使用 R 和 `rxDataStep` 函数    
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的自定义函数  
  
对于这两种方法，代码的结果将是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源对象 `featureDataSource`，其中包含新数字功能 `direct_distance`。  
  
## <a name="creating-features-using-r"></a>使用 R 创建功能  

虽然 R 语言以其丰富多样的统计库而闻名，但用户可能仍需创建自定义数据转换。 

+ 创建一个新的 R 函数 `ComputeDist`，用于计算纬度和经度值指定的两个点之间的直线距离。  
+ 调用该函数来转换先前创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据对象中的数据，并将其保存在新数据源 `featureDataSource` 中。  

### <a name="create-the-transformation-function"></a>创建转换函数  
1.  创建自定义 R 函数 `ComputeDist`。 该函数使用两对纬度和经度值，然后计算它们之间的直线距离。  该函数以英里为单位返回距离。
  
    ```R  
    env <- new.env()  
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){  
      R <- 6371/1.609344 #radius in mile  
      delta_lat <- dropoff_lat - pickup_lat  
      delta_long <- dropoff_long - pickup_long  
      degrees_to_radians = pi/180.0  
      a1 <- sin(delta_lat/2*degrees_to_radians)  
      a2 <- as.numeric(a1)^2  
      a3 <- cos(pickup_lat*degrees_to_radians)  
      a4 <- cos(dropoff_lat*degrees_to_radians)  
      a5 <- sin(delta_long/2*degrees_to_radians)  
      a6 <- as.numeric(a5)^2  
      a <- a2+a3*a4*a6  
      c <- 2*atan2(sqrt(a),sqrt(1-a))  
      d <- R*c  
      return (d)  
    }  
    ```  
  
    + 第一行定义一个新环境。 在 R 中，环境可用于将命名空间封装在包及类似对象中。
    + 可以使用 `search()` 函数查看工作区中的环境。 若要查看特定环境中的对象，请键入 `ls(<envname>)`。 
    + 以 `$env.ComputeDistance` 开头的行包含定义 haversine 公式的代码，该公式计算球面上两点之间的 *大圆距离* 。  
 
  
### <a name="apply-the-transformation-function-to-data"></a>对数据应用转换函数

定义函数后，可将其应用到数据，以创建新功能列 direct_distance。

1. 使用 `RxSqlServerData` 构造函数创建一个要使用的数据源。  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  调用 `rxDataStep` 函数将 `env$ComputeDist` 函数应用到指定的数据。  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + `rxDataStep` 函数可适当修改数据。 参数包括要传递的列的字符矢量 (*varsToKeep*)，以及一个定义转换的列表。
    + 经过转换的所有列都会自动输出，因此无需包含在 *varsToKeep* 参数中。
    + 或者，可以使用 *varsToDrop* 参数指定包含源中的所有列，指定的变量除外。  
  
4.  最后，调用 `rxGetVarInfo` 检查新数据源的架构：  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    结果
    
    “生成功能用时：CPU 时间=0.74 秒，占用时间=35.75 秒。”  
    变量 1：tipped，类型：整型   
    变量 2：fare_amount，类型：数值型   
    变量 3：passenger_count，类型：数值型   
    变量 4：trip_time_in_secs，类型：数值型   
    变量 5：trip_distance，类型：数值型   
    变量 6：pickup_datetime，类型：字符型   
    变量 7：dropoff_datetime，类型：字符型   
    变量 8：pickup_longitude，类型：数值型   
    变量 9：pickup_latitude，类型：数值型   
    变量 10：dropoff_longitude，类型：数值型   
    变量 11：dropoff_latitude，类型：数值型   
    变量 12：direct_distance，类型：数值型   
  
## <a name="creating-features-using-transact-sql"></a>使用 Transact-SQL 创建功能  
了解如何使用 R 函数创建功能后，将使用自定义 SQL 函数 `ComputeDist` 完成相同的任务。 SQL 函数 `ComputeDist` 对现有 `RxSqlServerData` 数据对象进行操作，以通过现有的纬度和经度值创建新的距离功能。  
  
将转换的结果保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据对象 `featureDataSource`，和使用 R 时的操作一样。  
  
使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的功能工程速度通常会比 R 快。请根据数据和任务选择最高效的方法。  

### <a name="define-the-t-sql-custom-function"></a>定义 T-SQL 自定义函数
  
1.  定义新的 SQL 函数 `fnCalculateDistance`  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END  
  
    ```  

    + 此 SQL *用户定义函数* 的代码作为 PowerShell 脚本的一部分提供，该脚本用于创建和配置数据库。  数据库中应该已存在该函数。  如果不存在，请使用 SQL Server Management Studio 在存储出租车数据的同一数据库中生成该函数。

2.  若要查看该函数的工作原理，请通过任何支持 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的应用程序查看下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>从 R 中调用 SQL 函数

1. 保存调用 R 变量中自定义函数的 SQL 语句。  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] 此查询与之前使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询略有不同。 它经过修改，可获取更小的数据样本，从而让本演练的速度变快。  
  
4.  现在，请使用下面的代码行来从 R 环境中调用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数，并将其应用于 `featureEngineeringQuery`中定义的数据。  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  新功能创建后，调用 `rxGetVarsInfo` 创建功能表的摘要。  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>比较 R 函数和 SQL 函数

事实证明，对于此特定任务， [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数方法的速度比自定义 R 函数快。 因此，将使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数在后续步骤中完成这些计算。  

请继续学习下一课，了解如何使用此数据生成预测模型并将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
## <a name="next-lesson"></a>下一课  
[第 4 课：生成并保存模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 2 课：查看和浏览数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
