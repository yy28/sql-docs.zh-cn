---
title: "创建使用 R 和 SQL （演练） 的数据功能 |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 79cc7e334c3aab4fb7702e368a3188db98eaaced
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>创建使用 R 和 SQL （演练） 的数据功能

数据工程是机器学习的一个重要组成部分。 数据通常需要转换，然后才能使用它进行预测性建模。 如果数据不具有所需的功能，可根据现有值进行创建。

对于此建模任务，想要以英里表示的上车和下车位置之间的距离，而不是使用这两个位置的原始纬度和经度值。 若要创建此功能，你计算通过使用两个点之间的直接线性距离[haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)。

在此步骤中，我们将比较两个不同的方法，用于从数据中创建一项功能：

- 使用自定义 R 函数
- 使用中的自定义 T-SQL 函数[!INCLUDE[tsql](../../includes/tsql-md.md)]

目的是创建一个新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组数据，包括原始列加上新的数字特征， *direct_distance*。

## <a name="featurization-using-r"></a>使用 R 的特征

虽然 R 语言以其丰富多样的统计库而闻名，但用户可能仍需创建自定义数据转换。

首先，让我们开始吧在用户的方式 R 习惯： 获取到便携式计算机、 数据，然后运行自定义 R 函数， *ComputeDist*，其计算由纬度和经度值指定的两个点之间的线性距离。

1. 请记住你之前创建的数据源对象获取仅前 1000年行。 因此，让我们定义获取所有数据的查询。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 创建新的 SQL Server 数据源使用查询。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可以包含有效的 SELECT 查询中，作为自变量提供的任一查询_sqlQuery_参数或表对象，作为提供的名称_表_参数。
    
    - 如果你希望示例数据从一个表，则必须使用_sqlQuery_参数，定义采样参数使用 T-SQL 的 TABLESAMPLE 子句中，并设置_rowBuffering_为 FALSE 的参数。

3. 运行以下代码以创建自定义 R 函数。 ComputeDist 采用的纬度和经度值的两个对，并计算它们在英里返回距离之间的线性距离。

    ```R
    env <- new.env();
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
  
    + 第一行定义一个新环境。 在 R 中，环境可用于将命名空间封装在包及类似对象中。  可以使用 `search()` 函数查看工作区中的环境。 若要查看特定环境中的对象，请键入 `ls(<envname>)`。
    + 以 `$env.ComputeDistance` 开头的行包含定义 haversine 公式的代码，该公式计算球面上两点之间的 *大圆距离* 。

4. 具有定义的函数，你将其应用于数据以创建新的特征列， *direct_distance*。 但在运行转换之前，将计算上下文更改为本地。

    ```R
    rxSetComputeContext("local");
    ```

5. 调用[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函数获取工程数据，该功能并应用`env$ComputeDist`到内存中的数据的函数。

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + RxDataStep 函数支持各种方法来在位置中修改数据。 有关详细信息，请参阅此文章：[如何转换和子集 Microsft R 中的数据](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    但是，值得注意有关 rxDataStep 有几点： 
    
    在其他数据源，你可以使用自变量*varsToKeep*和*varsToDrop*，但对于 SQL Server 数据源不支持这些。 因此，在此示例中，我们已使用_转换_自变量以指定的传递列和转换后的列。 此外，当 SQL Server 中的运行计算上下文， _inData_参数只能接受 SQL Server 数据源。

    前面的代码还可以生成一条警告消息，当在大型数据集上运行。 数乘积的行数的列正在创建超过设定的值 （默认值为 3,000,000）、 rxDataStep 返回一条警告，并返回的数据帧中的行数将被截断。 若要删除此警告，可以修改_maxRowsByCols_ rxDataStep 函数中的参数。 但是，如果_maxRowsByCols_太大，加载到内存中的数据帧时，可能会遇到问题。

7. （可选） 可以调用[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)检查转换的数据源的架构。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 进行功能化

现在，创建一个自定义的 SQL 函数， *ComputeDist*，以完成相同任务的自定义 R 函数。

1. 定义一个名为 fnCalculateDistance 的新的自定义 SQL 函数。 用户定义的此 SQL 函数的代码作为你创建和配置数据库时运行的 PowerShell 脚本的一部分提供。  数据库中应该已存在该函数。

    如果不存在，请使用 SQL Server Management Studio 在存储出租车数据的同一数据库中生成该函数。

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
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

2. 从支持 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的任何应用程序运行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，查看该函数如何工作。

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. 定义了此函数后，它可以很容易地创建要通过使用 SQL 的功能，然后将值直接插入新表：

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 但是，让我们了解如何从 R 代码调用自定义的 SQL 函数。 首先，R 变量中存储 SQL 特征化查询。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 已修改此查询来获取数据，以使本演练更快的较小示例。 如果你想要获取所有的数据; 可以删除 TABLESAMPLE 子句但是，具体取决于你的环境，它可能不能加载到 R，从而导致错误的完整数据集。
  
5. 使用下面的代码行来从 R 环境中调用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数，并将其应用于 featureEngineeringQuery 中定义的数据。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  创建新的功能后，调用**rxGetVarsInfo**在 feature 表中创建的数据摘要。
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *结果*

    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > 在某些情况下，你可能会与此类似的错误： *EXECUTE 权限已拒绝了对对象 fnCalculateDistance*如果是这样，请确保你使用的登录名有权运行脚本并在数据库中，创建对象不只是基于实例。
    > 检查的对象，fnCalculateDistance 的架构。 如果对象由数据库所有者，并且你的登录名属于角色 db_datareader，你需要为登录提供显式权限来运行脚本。

## <a name="comparing-r-functions-and-sql-functions"></a>比较 R 函数和 SQL 函数

请记住此段代码用于时间的 R 代码？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

你可以尝试使用此 SQL 自定义函数的示例使用以查看数据转换的时间调用 SQL 函数时。 此外，请尝试切换与 rxSetComputeContext 计算上下文，并比较计时。

你的时间可能差异很大，具体取决于你网络的速度和你的硬件配置。 在我们测试的配置[!INCLUDE[tsql](../../includes/tsql-md.md)]函数的方法是比使用自定义 R 函数更快。 因此，我们已使用[!INCLUDE[tsql](../../includes/tsql-md.md)]这些计算在随后的步骤的函数。

> [!TIP]
> 通常，功能工程使用[!INCLUDE[tsql](../../includes/tsql-md.md)]会更快比。例如，T-SQL 包括快速窗口和可以应用于如滚动移动平均线的常见数据科学计算的排名函数和 *n* -磁贴。 请根据你的数据和任务选择最高效的方法。

## <a name="next-lesson"></a>下一课

[生成 R 模型并将保存到 SQL](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>上一课

[查看和使用 R 汇总数据](walkthrough-view-and-summarize-data-using-r.md)

