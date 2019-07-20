---
title: 使用 R 和 SQL Server 函数创建数据功能
description: 介绍如何使用 SQL Server 函数为数据库内分析创建数据功能的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: a7d62004745f8b77bbc26b4d924e2e3948cf2f9e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345835"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>使用 R 和 SQL Server 创建数据功能 (演练)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据工程是机器学习的一个重要组成部分。 数据通常需要转换, 然后才能将其用于预测建模。 如果数据不具有所需的功能，可根据现有值进行创建。

对于此建模任务，想要以英里表示的上车和下车位置之间的距离，而不是使用这两个位置的原始纬度和经度值。 若要创建此功能, 请使用[半正矢公式](https://en.wikipedia.org/wiki/Haversine_formula)计算两个点之间的直接线性距离。

在此步骤中, 将了解从数据创建功能的两种不同方法:

> [!div class="checklist"]
> * 使用自定义 R 函数
> * 在中使用自定义 T-sql 函数[!INCLUDE[tsql](../../includes/tsql-md.md)]

目标是创建一组新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据, 其中包括原始列和新的数字功能*direct_distance*。

## <a name="prerequisites"></a>系统必备

此步骤假设正在进行的 R 会话基于本演练中前面的步骤。 它使用在这些步骤中创建的连接字符串和数据源对象。 以下工具和包用于运行脚本。

+ Rgui.exe 运行 R 命令
+ Management Studio 运行 T-sql

## <a name="featurization-using-r"></a>使用 R 特征化

虽然 R 语言以其丰富多样的统计库而闻名，但用户可能仍需创建自定义数据转换。

首先, 让我们来看看用户习惯: 将数据获取到便携式计算机, 然后运行自定义 R 函数*ComputeDist*, 该函数计算纬度值和经度值所指定的两个点之间的线性距离。

1. 请记住, 先前创建的数据源对象只获取前1000行。 接下来, 让我们定义一个查询来获取所有数据。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 使用查询创建新的数据源对象。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可以采用包含有效 SELECT 查询的查询, 作为_sqlQuery_参数的参数提供, 或作为_表_参数提供的表对象的名称。
    
    - 如果要对表中的数据进行采样, 则必须使用_sqlQuery_参数, 使用 t-sql TABLESAMPLE 子句定义采样参数, 并将_rowBuffering_参数设置为 FALSE。

3. 运行以下代码以创建自定义 R 函数。 ComputeDist 采用两对纬度和经度值, 并计算它们之间的线性距离, 返回以英里为单位的距离。

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
  
    + 第一行定义一个新环境。 在 R 中，环境可用于将命名空间封装在包及类似对象中。 可以使用 `search()` 函数查看工作区中的环境。 若要查看特定环境中的对象，请键入 `ls(<envname>)`。
    + 以 `$env.ComputeDist` 开头的行包含定义 haversine 公式的代码，该公式计算球面上两点之间的 *大圆距离* 。

4. 定义函数后, 可将其应用到数据, 以创建新的功能列*direct_distance*。 但在运行转换之前, 将计算上下文更改为 "本地"。

    ```R
    rxSetComputeContext("local");
    ```

5. 调用[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函数以获取特性工程数据, 并将`env$ComputeDist`函数应用于内存中的数据。

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
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

    + RxDataStep 函数支持多种方法来就地修改数据。 有关详细信息, 请参阅以下文章:[如何在 Microsft R 中转换和子集化数据](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    不过, 有几个值得注意的要点 rxDataStep: 
    
    在其他数据源中, 可以使用参数*varsToKeep*和*varsToDrop*, 但 SQL Server 数据源不支持这些参数。 因此, 在此示例中, 我们使用了_转换_参数来指定传递列和转换后的列。 此外, 在 SQL Server 计算上下文中运行时, _inData_参数只能采用 SQL Server 的数据源。

    在较大的数据集上运行时, 上述代码还可以生成警告消息。 当行数乘以所3000000创建的列数时, 将会返回一个警告, 并且返回的数据帧中的行数将被截断。 若要删除此警告, 可以修改 rxDataStep 函数中的_maxRowsByCols_参数。 但是, 如果_maxRowsByCols_太大, 则在将数据帧加载到内存中时可能会遇到问题。

7. 或者, 您可以调用[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)来检查转换后的数据源的架构。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 进行功能化

在此练习中, 将了解如何使用 SQL 函数 (而不是自定义 R 函数) 完成相同的任务。 

切换到[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或另一个查询编辑器来运行 t-sql 脚本。

1. 使用名为*fnCalculateDistance*的 SQL 函数。 该函数应已存在于 NYCTaxi_Sample 数据库中。 在对象资源管理器中, 通过导航以下路径来验证该函数是否存在:数据库 > NYCTaxi_Sample > 可编程性 > 函数 > 标量值函数 > fnCalculateDistance。

    如果该函数不存在, 请使用 SQL Server Management Studio 在 NYCTaxi_Sample 数据库中生成该函数。

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

2. 在 Management Studio 中, 在新的查询窗口中, 从[!INCLUDE[tsql](../../includes/tsql-md.md)]支持[!INCLUDE[tsql](../../includes/tsql-md.md)]的任何应用程序运行以下语句, 以查看函数的工作原理。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 若要将值直接插入到新表中 (必须首先创建), 可以添加一个**into**子句来指定表名称。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 你还可以从 R 代码中调用 SQL 函数。 切换回 Rgui.exe, 并在 R 变量中存储 SQL 特征化查询。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 已将此查询修改为获取较小的数据示例, 以便更快地完成此演练。 如果要获取所有数据, 则可以删除 TABLESAMPLE 子句;但是, 根据您的环境, 可能无法将完整的数据集加载到 R 中, 导致错误。
  
5. 使用下面的代码行来从 R 环境中调用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数，并将其应用于 featureEngineeringQuery  中定义的数据。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  创建新功能后, 请调用**rxGetVarsInfo**来创建功能表中的数据摘要。
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **结果**

    ```R
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
    > 在某些情况下, 可能会收到类似于下面的错误:*拒绝了对对象 ' fnCalculateDistance ' 的 EXECUTE 权限*如果是这样, 请确保您使用的登录名有权在数据库上运行脚本和创建对象, 而不只是在实例上运行。
    > 检查对象的架构 fnCalculateDistance。 如果该对象是由数据库所有者创建的, 并且你的登录名属于角色 db_datareader, 则需要为登录名授予显式权限才能运行该脚本。

## <a name="comparing-r-functions-and-sql-functions"></a>比较 R 函数和 SQL 函数

请记住此代码段用于时间 R 代码吗？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

可以尝试将此与 SQL 自定义函数示例一起使用, 以查看调用 SQL 函数时数据转换所用的时间。 同时, 尝试通过 rxSetComputeContext 切换计算上下文, 并比较计时。

根据网络速度和硬件配置, 时间可能会有很大的差异。 在我们测试的配置中, [!INCLUDE[tsql](../../includes/tsql-md.md)]函数方法比使用自定义 R 函数快。 因此, 在后续步骤中[!INCLUDE[tsql](../../includes/tsql-md.md)] , 我们已将函数用于这些计算。

> [!TIP]
> 通常, 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的功能工程比 R 快。例如, T-sql 包含快速的窗口化和排名函数, 这些函数可应用于常见的数据科学计算, 例如滚动移动平均线和*n*磁贴。 请根据你的数据和任务选择最高效的方法。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [生成 R 模型并保存到 SQL](walkthrough-build-and-save-the-model.md)

