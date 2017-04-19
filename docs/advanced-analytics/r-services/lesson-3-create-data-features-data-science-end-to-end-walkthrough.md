---
title: "第 3 课：创建数据功能（数据科学端到端演练）| Microsoft Docs"
ms.custom: 
ms.date: 11/22/2016
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ffdb1c199ae81a421b80c07b12d2da8ba3d32b3d
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-3-create-data-features-data-science-end-to-end-walkthrough"></a>第 3 课：创建数据功能（数据科学端到端演练）
数据工程是机器学习的一个重要组成部分。 通常需要先转换数据，然后才能使用数据进行预测建模。 如果数据不具有所需的功能，可根据现有值进行创建。  
  
对于此建模任务，想要以英里表示的上车和下车位置之间的距离，而不是使用这两个位置的原始纬度和经度值。 若要创建此功能，需要使用 [haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)计算两个点之间的直线距离。  

将比较用于通过数据创建功能的两个不同方法：  
  
-   使用 R 和 rxDataStep 函数    
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的自定义函数  
  
对于这两种方法，代码的结果都是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源对象 featureDataSource，其中包含新数字功能 direct_distance。  
  
## <a name="featurization-using-r"></a>使用 R 进行功能化  

虽然 R 语言以其丰富多样的统计库而闻名，但用户可能仍需创建自定义数据转换。 

+ 你将创建一个新的 R 函数 ComputeDist，用于计算纬度和经度值指定的两个点之间的直线距离。  
+ 你将调用该函数来转换先前创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据对象中的数据，并将其保存在新数据源 featureDataSource 中。  


1.  运行以下代码来创建自定义 R 函数 ComputeDist。 该函数使用两对纬度和经度值，然后计算它们之间的直线距离。  该函数以英里为单位返回距离。
  
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
 
    定义函数后，可将其应用到数据，以创建新功能列 direct_distance 。 

2. 使用 RxSqlServerData 构造函数创建一个要使用的数据源。  
  
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
  
3.  调用 rxDataStep 函数将 `env$ComputeDist` 函数应用到指定的数据。  
    
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
  
    + rxDataStep 函数可适当修改数据。 参数包括要传递的列的字符矢量 (*varsToKeep*)，以及一个定义转换的列表。
    + 经过转换的所有列都会自动输出，因此无需包含在 *varsToKeep* 参数中。
    + 或者，可以使用 *varsToDrop* 参数指定包含源中的所有列，指定的变量除外。  
  
4.  调用 rxGetVarInfo 检查新数据源的架构：  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *结果*
    
    “生成功能用时：CPU 时间=0.74 秒，占用时间=35.75 秒。”  
    变量 1：tipped，类型：整型   
       
       
       
       
       
       
       
       
       
    变量 11：dropoff_latitude，类型：数值型   
    变量 12：direct_distance，类型：数值型   
  
## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 进行功能化  

现在，你将创建一个自定义 SQL 函数 ComputeDist，用以执行刚才创建的 R 函数所执行的相同操作。 自定义 SQL 函数 ComputeDist 对现有 RxSqlServerData 数据对象进行操作，以通过现有的纬度和经度值创建新的距离功能。  
  
然后，你将转换的结果保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据对象 featureDataSource，和使用 R 时的操作一样。 
  
1.  定义一个名为 fnCalculateDistance 的新的自定义 SQL 函数。  
  
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

    + 用户定义的此 SQL 函数的代码作为你创建和配置数据库时运行的 PowerShell 脚本的一部分提供。  数据库中应该已存在该函数。  如果不存在，请使用 SQL Server Management Studio 在存储出租车数据的同一数据库中生成该函数。

2.  从支持 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的任何应用程序运行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，查看该函数如何工作。 
  
    ```sql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
3.  若要在 R 代码中使用自定义 SQL 函数，请将功能工程查询保存在一个 R 变量中。  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP]
    > 此查询与之前使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询略有不同。 它经过修改，可获取更小的数据样本，从而让本演练的速度变快。  
  
4. 使用下面的代码行来从 R 环境中调用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数，并将其应用于 featureEngineeringQuery 中定义的数据。  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  现在，新功能已创建，请调用 rxGetVarsInfo 来创建功能表的摘要。  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>比较 R 函数和 SQL 函数

事实证明，对于此特定任务， [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数方法的速度比自定义 R 函数快。 因此，将使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数在后续步骤中完成这些计算。  

请继续学习下一课，了解如何使用此数据生成预测模型并将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  

> [!TIP]
> 通常，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的功能工程将比 R 更快。例如，T-SQL 包括了在数据科学家经常在 R 中执行的任务中非常快的窗口化和排名函数，例如滚动移动平均值和 ntiles。 请根据你的数据和任务选择最高效的方法。  

  
## <a name="next-lesson"></a>下一课  
[第 4 课：生成并保存模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 2 课：查看和浏览数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  


