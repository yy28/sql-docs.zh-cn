---
title: 使用 R 和 SQL Server 功能-SQL Server 机器学习创建数据功能
description: 本教程演示如何使用 SQL Server 函数的数据库内分析创建数据功能。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 609896357845aa4f466e874524b8136b34e32b9a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511694"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>使用 R 和 SQL Server （演练） 创建数据功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据工程是机器学习的一个重要组成部分。 数据通常需要转换，然后才能使用它进行预测建模。 如果数据不具有所需的功能，可根据现有值进行创建。

对于此建模任务，想要以英里表示的上车和下车位置之间的距离，而不是使用这两个位置的原始纬度和经度值。 若要创建此功能，则计算两个点，通过使用之间的直线距离[半正矢公式](https://en.wikipedia.org/wiki/Haversine_formula)。

在此步骤中，了解用于从数据创建一项功能的两种不同方法：

> [!div class="checklist"]
> * 使用自定义 R 函数
> * 使用中的自定义 T-SQL 函数 [!INCLUDE[tsql](../../includes/tsql-md.md)]

目标是创建一个新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包含的原始列和新数字功能的数据集*direct_distance*。

## <a name="prerequisites"></a>先决条件

此步骤假定正在进行 R 会话基于本演练中之前的步骤。 它使用这些步骤中创建的连接字符串和数据源对象。 使用以下工具和包来运行脚本。

+ 若要运行 R 命令的 Rgui.exe
+ Management Studio 来运行 T-SQL

## <a name="featurization-using-r"></a>使用 R 进行功能化

虽然 R 语言以其丰富多样的统计库而闻名，但用户可能仍需创建自定义数据转换。

首先，让我们开始吧方式 R 用户习惯： 获取到您的便携式计算机上的数据，然后运行自定义 R 函数*ComputeDist*，其计算指定的纬度和经度值的两个点之间的直线距离。

1. 请记住前面创建的数据源对象获取只显示前 1000年行。 因此，让我们定义一个查询，获取所有数据。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 创建新的数据源对象使用的查询。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可能需要包含有效的 SELECT 查询中作为参数提供的任一查询_sqlQuery_参数或与提供的表对象的名称_表_参数。
    
    - 如果你希望示例数据从一个表，则必须使用_sqlQuery_参数，定义采样参数使用 T-SQL TABLESAMPLE 子句中，并设置_rowBuffering_参数为 FALSE。

3. 运行以下代码以创建自定义 R 函数。 ComputeDist 函数使用两对纬度和经度值，并计算它们返回中英里的距离之间的直线距离。

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

4. 定义函数后，您将其应用于要创建新的功能列的数据*direct_distance*。 但在运行转换之前，将计算上下文更改为本地。

    ```R
    rxSetComputeContext("local");
    ```

5. 调用[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函数获取特征工程数据，并应用`env$ComputeDist`到内存中的数据的函数。

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

    + RxDataStep 函数支持位置中修改数据的各种方法。 有关详细信息，请参阅这篇文章：[如何转换和子集 Microsft R 中的数据](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    但是，一些值得注意有关 rxDataStep 的要点： 
    
    在其他数据源，您可以使用参数*varsToKeep*并*varsToDrop*，但这些不受支持的 SQL Server 数据源。 因此，在此示例中，我们使用_转换_参数，以指定的传递列和转换后的列。 此外，当运行在 SQL Server 计算上下文中， _inData_参数仅可使用 SQL Server 数据源。

    前面的代码还可以生成更大的数据集上运行时，一条警告消息。 时的行数乘以数量的列创建超过设定的值 （默认值为 3000000）、 rxDataStep 返回一条警告，并返回的数据帧中的行数将被截断。 若要消除该警告，可以修改_maxRowsByCols_ rxDataStep 函数中的参数。 但是，如果_maxRowsByCols_太大，数据帧加载到内存时，可能会遇到问题。

7. （可选） 可以调用[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)检查转换后的数据源的架构。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 进行功能化

在此练习中，了解如何完成相同的任务而不自定义 R 函数使用 SQL 函数。 

切换到[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或另一个查询编辑器来运行 T-SQL 脚本。

1. 使用一个名为的 SQL 函数*fnCalculateDistance*。 该函数应已存在于 NYCTaxi_Sample 数据库。 在对象资源管理器，验证存在通过导航此路径的函数：数据库 > NYCTaxi_Sample > 可编程性 > 函数 > 标量值函数 > dbo.fnCalculateDistance。

    如果该函数不存在，请使用 SQL Server Management Studio NYCTaxi_Sample 数据库中生成该函数。

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

2. 在 Management Studio 中，在新查询窗口中，运行以下[!INCLUDE[tsql](../../includes/tsql-md.md)]从任何应用程序支持的语句[!INCLUDE[tsql](../../includes/tsql-md.md)]若要查看函数的工作方式。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 若要将值直接插入新表中 （您需要首先创建），可以添加**INTO**子句，用于指定表名。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 您还可以从 R 代码中调用 SQL 函数。 切换回 Rgui 并在一个 R 变量中存储 SQL 特征化查询。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 已修改此查询以获取较小数据，以更快地使本演练的示例。 如果你想要获取所有数据; 可以删除 TABLESAMPLE 子句但是，具体取决于你的环境，它可能无法加载到 R，从而导致错误的完整数据集。
  
5. 使用下面的代码行来从 R 环境中调用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数，并将其应用于 featureEngineeringQuery 中定义的数据。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  创建新的功能，请调用**rxGetVarsInfo**功能表中创建的数据的摘要。
  
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
    > 在某些情况下，可能会收到如下错误：*EXECUTE 权限被拒绝的对象 fnCalculateDistance*如果是这样，请确保你使用的登录名有权运行脚本以及在数据库上，而不仅仅是在实例上创建对象。
    > 检查对象，fnCalculateDistance 的架构。 如果你的登录名都属于角色 db_datareader 由数据库所有者，创建对象时，您需要为该登录名提供明确的权限以运行该脚本。

## <a name="comparing-r-functions-and-sql-functions"></a>比较 R 函数和 SQL 函数

请记住此代码用于 R 代码的时间段？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

可以尝试使用此 SQL 自定义函数示例请参阅数据转换需要花多长时调用 SQL 函数。 此外，请尝试切换计算上下文使用 rxSetComputeContext 并比较计时。

你的时间可能差异很大，具体取决于您的网络速度，以及您的硬件配置。 在我们测试的配置[!INCLUDE[tsql](../../includes/tsql-md.md)]函数的方法是速度快于使用自定义 R 函数。 因此，我们将使用[!INCLUDE[tsql](../../includes/tsql-md.md)]在后续步骤中的这些计算的函数。

> [!TIP]
> 通常，功能工程使用[!INCLUDE[tsql](../../includes/tsql-md.md)]速度将快比。例如，T-SQL 包括快速窗口化和排名函数，可应用于常见数据科学计算，例如滚动移动平均值和*n*-磁贴。 请根据你的数据和任务选择最高效的方法。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [生成 R 模型并将保存到 SQL](walkthrough-build-and-save-the-model.md)

