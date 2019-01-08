---
title: 查看和汇总 SQL Server 数据使用 R 函数的 SQL Server 机器学习
description: 本教程说明如何可视化和生成的 SQL Server 上的数据库内分析中使用 R 函数的统计摘要。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 368caa21545e534c393aca29ce8fd3a59f9d9837
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644556"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>查看和汇总 SQL Server 数据使用 R （演练）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程向您介绍中的函数**RevoScaleR**打包并指导你完成以下任务：

> [!div class="checklist"]
> * 连接到 SQL Server
> * 定义具有所需数据的查询或指定表或视图
> * 定义当运行 R 代码时要使用的一个或多个计算上下文
> * （可选） 定义了从源读取时应用于数据源的转换

## <a name="define-a-sql-server-compute-context"></a>定义 SQL Server 计算上下文

客户端工作站上的 R 环境中运行以下 R 语句。 本部分假设[使用 Microsoft R 客户端数据科学工作站](../r/set-up-a-data-science-client.md)，因为它包括所有 RevoScaleR 包，以及一套基本、 轻量的 R 工具。 例如，可以使用 Rgui.exe 在本部分中运行 R 脚本。

1. 如果**RevoScaleR**包已加载，则运行此 R 代码行：

    ```R
    library("RevoScaleR")
    ```

     引号是可选的在这种情况下，尽管建议。
     
     如果遇到错误，请确保你的 R 开发环境正在使用的库中包含的 RevoScaleR 包。 使用命令如`.libPaths()`若要查看当前的库路径。

2. 为 SQL Server 创建连接字符串并将其保存在一个 R 变量*connStr*。

   必须将占位符"your_server_name"更改为有效的 SQL Server 实例名称。 对于服务器名称中，您可能能够使用只是实例名称，或可能需要完全限定的名称，具体取决于你的网络。
    
   SQL Server 身份验证的连接语法如下所示：

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    对于 Windows 身份验证的语法是稍有不同：
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    通常情况下，我们建议在可能的情况，以避免将密码保存在 R 代码中使用 Windows 身份验证。

3. 定义要用于创建一个新的变量*计算上下文*。 创建计算上下文对象后，可用于 SQL Server 实例上运行 R 代码。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机之间来回序列化 R 对象时，R 会使用临时目录。 可指定用作 sqlShareDir 的本地目录，或者接受默认目录。
  
    - 使用*sqlWait*以指示您是否要 R 等待来自服务器的结果。  与非等待作业正在等待的讨论，请参阅[分布式计算和使用 Microsoft R 中的 RevoScaleR 的并行计算](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用参数*sqlConsoleOutput*以指示您不想要查看从 R 控制台的输出。

4. 在调用[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)构造函数来创建计算上下文对象的变量和连接字符串已定义，并将新对象保存在 R 变量*sqlcc*。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 默认情况下，计算上下文位于本地，因此需要显式设置*active*计算上下文。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)不可见的方式返回之前处于活动状态的计算上下文，以便您可以使用它
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)返回活动的计算上下文
    
    请注意，设置计算上下文仅影响使用中的函数的操作**RevoScaleR**包; 该计算上下文不会影响执行开源 R 运算的方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>创建使用 RxSqlServer 数据源

使用 RevoScaleR 和 MicrosoftML，等的 Microsoft R 库时*数据源*是使用 RevoScaleR 函数创建的对象。 数据源对象指定某些想要使用的一个任务，例如模型训练或特征提取的数据的集。 您可以从各种来源包括 SQL Server 获取数据。 当前支持的源的列表，请参阅[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

前面定义连接字符串，并在一个 R 变量中保存该信息。 您可以重新使用该连接信息以指定的数据要获取。

1. 将 SQL 查询保存为一个字符串变量。 查询定义用于定型模型的数据。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我们使用了 TOP 子句来使操作运行得更快，但由查询返回的实际行根据顺序可能有所不同。 因此，摘要结果也可能不同于下面所列。 可以删除 TOP 子句。

2. 将查询定义作为参数传递到 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 函数。

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + colClasses   参数指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 间移动数据时要使用的列类型。这一点非常主要，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的数据类型不同于 R，且使用的数据类型更多。 有关详细信息，请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。
  
    + 自变量*rowsPerRead*对于管理内存使用率和高效计算非常重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中大多数增强的分析函数都可以处理区块中的数据并累积中间结果，并在读取所有的数据后返回最终的计算。  通过添加*rowsPerRead*参数，可以控制数据的行数读入每个区块中进行处理。  如果此参数的值太大，数据访问可能很慢，因为你没有足够的内存来有效地处理此类较大的数据块。  在某些系统中，设置*rowsPerRead*为过小的值还可以提供性能下降。

3. 此时，已创建*inDataSource*对象，但它不包含任何数据。 数据才会被提取的 SQL 查询从本地环境到如运行函数之后，才能[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)。

    但是，现在，已定义的数据对象，您可以使用它作为其他函数的参数。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 R 摘要中的 SQL Server 数据

在本部分中，你将尝试中提供的函数的几个[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]支持远程计算上下文。 通过将 R 函数应用到数据源，可以浏览、 总结和绘制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。

1. 调用函数[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)以获取中的数据源及其数据类型的变量的列表。

    **rxGetVarInfo**是一个便捷函数; 您可以在任何数据帧上调用它或的远程数据对象中的数据集中，以获取信息，例如最大值和最小值，数据类型和因子列中的级别数。
    
    请考虑在进行任何类型的数据输入、功能转换或功能工程后运行此函数。 通过执行此操作，可以确保所有想要使用它在模型中的功能都是所需的数据类型，并避免错误。
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **结果**
    
    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. 现在，调用 RevoScaleR 函数[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)以获取有关各个变量的详细统计信息。

    rxSummary 基于 R`summary`函数，但有一些其他功能和优点。 rxSummary 在多个计算上下文中并支持分块。  此外可以使用 rxSummary 来转换值，或汇总基于的因素级别。
    
    在此示例中，您可以汇总基于乘客数量为费用金额。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一个参数指定的公式或字词汇总方式。 在这里，`F()`函数用于中的值转换为_乘客\_计数_为之前汇总的因素。 您还必须指定的最小值 (1) 和最大值 (6) 用于_乘客\_计数_因子变量。
    + 如果未指定要输出的统计信息，默认情况下 rxSummary 输出平均值、 StDev、 Min、 Max 和有效且缺失的观察值。
    + 本示例中也包括跟踪函数开始时间和完成时间的代码，以便可以比较性能。
  
    **结果**

    如果 rxSummary 函数成功运行，应看到如下，结果按类别后跟的统计信息列表。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>对大数据的附加练习

请尝试定义的所有行的新查询字符串。 我们建议你设置新的数据源对象对于此试验。 您还可以尝试更改*rowsToRead*参数，以查看它如何影响吞吐量。

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> 在此运行时，可以使用之类的工具[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx)或使用 SQL Server 服务运行 SQL Profiler，若要查看如何建立连接和 R 代码。
> 
> 另一个选项是监视使用这些 SQL Server 上运行的 R 作业[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 创建图形和绘图](walkthrough-create-graphs-and-plots-using-r.md)