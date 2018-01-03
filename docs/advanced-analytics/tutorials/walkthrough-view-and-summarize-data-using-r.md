---
title: "查看和使用 R （演练） 汇总数据 |Microsoft 文档"
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: "22"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 37d73022a1e45c5166bec70bb68f6bf3b995345e
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="view-and-summarize-data-using-r"></a>查看和使用 R 汇总数据

现在让我们使用相同的数据使用 R 代码。 在本课程中，您将学习如何使用中的函数**RevoScaleR**包。

本演练提供的 R 脚本包括创建数据对象、生成摘要和生成模型所需的所有代码。 R 脚本文件 **RSQL_RWalkthrough.R**位于脚本文件的安装位置。

+ 如果熟悉 R，则可同时运行所有脚本。
+ 对于学习使用 RevoScaleR 的读者，本教程将经历脚本行的行。
+ 若要运行此脚本中的各个行，可突出显示文件中的行，然后按 Ctrl + Enter。

> [!TIP]
> 保存 R 工作区，以防你想要稍后完成本演练的剩余部分。  通过这种方式的数据对象和其他变量是供重复使用。

## <a name="define-a-sql-server-compute-context"></a>定义 SQL Server 计算上下文

Microsoft R 可以轻松地从获取数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 R 代码中使用。 该过程如下所示：
  
- 创建与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接
- 定义具有所需数据的查询或指定表或视图
- 定义当运行 R 代码时要使用的一个或多个计算上下文
- （可选） 定义了在从源读取它时应用于数据源的转换

以下步骤在 R 代码中的一部分，并且应在 R 环境中运行。 我们使用 Microsoft R 客户端，因为它包含所有 RevoScaleR 包，以及一套基本、 轻量的 R 工具。

1. 如果**RevoScaleR**包尚未加载，运行此 R 代码行：

    ```R
    library("RevoScaleR")
    ```

     引号是可选的在这种情况下，不过，建议。
     
     如果遇到错误，请确保你的 R 开发环境正在使用库包括 RevoScaleR 包。 使用命令，例如`.libPaths()`查看当前的库路径。

2. 为 SQL Server 创建的连接字符串并将其保存在 R 变量中， _connStr_。
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=Your_Database_Name;Uid=Your_User_Name;Pwd=Your_Password"
    ```

    对于服务器名称中，你可能能够使用只是实例名称，或可能需要完全限定名称，具体取决于你的网络。

    对于 Windows 身份验证的语法是稍有不同：
    
    ```R
    connStr <- "Driver=SQL Server;Server=SQL_instance_name;Database=database_name;Trusted_Connection=Yes"
    ```

    供下载的 R 脚本仅使用 SQL 登录名。 通常情况下，我们建议你使用 Windows 身份验证，如果可能，以免在 R 代码中保存密码。 但是，若要确保在本教程中的代码与从 Github 下载的代码匹配，我们将演练的其余部分使用的 SQL 登录名。

3. 定义变量可用于创建一个新_计算上下文_。 创建计算上下文对象后，可用于 SQL Server 实例上运行 R 代码。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机之间来回序列化 R 对象时，R 会使用临时目录。 可指定用作 sqlShareDir 的本地目录，或者接受默认目录。
  
    - 使用*sqlWait*以指示你要 R 等待来自服务器的结果。  与非等待作业正在等待的讨论，请参阅[分布式和并行计算与 Microsoft R 中 ScaleR](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用参数*sqlConsoleOutput*以指示你不想以查看从 R 控制台的输出。


4. 你调用[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)构造函数的变量和连接字符串已定义，创建计算上下文对象，并将新对象保存在 R 变量*sqlcc*。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 默认情况下，计算上下文是本地计算机，因此你需要显式设置*active*计算上下文。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` 会无形返回先前活动的计算上下文，使其可供使用
    + `rxGetComputeContext` 返回活动的计算上下文
    
    请注意，设置计算上下文仅影响使用 **RevoScaleR** 包中的函数的操作；该计算上下文不会影响开源代码 R 操作的执行方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>创建数据源使用 RxSqlServer

Microsoft R 中*数据源*是使用 RevoScaleR 函数创建的对象。 数据源对象指定你想要使用的任务，例如模型定型或功能提取的数据的某些组。 你可以从各种源; 获取数据当前支持的源的列表，请参阅[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

前面你定义一个连接字符串，并且将该信息保存 R 变量中。 你可以重新使用该连接信息以指定的数据要获取。

1. 将 SQL 查询保存为一个字符串变量。 查询定义用于定型模型的数据。

    ```R
    sampleDataQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我们已使用 TOP 子句以使运行速度更快，但查询返回的实际行可以有所不同具体取决于顺序。 因此，摘要结果还可能与下面列出的有所不同。 请尝试删除 TOP 子句。

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
  
    + 自变量*rowsPerRead*对于管理内存使用情况和高效的计算很重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中大多数增强的分析函数都可以处理区块中的数据并累积中间结果，并在读取所有的数据后返回最终的计算。  通过添加*rowsPerRead*参数，你可以控制如何很多行数据读取到处理每个区块。  如果此参数的值太大，则数据访问可能很慢，因为没有足够的内存来有效地处理如此大型的数据区块。  在某些系统，设置*rowsPerRead*为过小的值还可以提供性能变慢。

3. 此时，你已创建*inDataSource*对象，但它不包含任何数据。 数据不从提取的 SQL 查询到本地环境之前运行函数如[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)。

    但是，现在，已定义数据对象，你可以使用它为其他函数的参数。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 R 摘要中的 SQL Server 数据

在此部分中，您将尝试进行多个中提供的函数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]该支持远程计算上下文。 通过将 R 函数应用于数据源，你可以浏览、 总结和图表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。

1. 调用函数[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)来获取数据源和其数据类型中的变量的列表。

    **rxGetVarInfo**是方便函数; 可以对任何数据帧，调用它或上的远程数据对象中的数据集，以获取信息，例如最大值和最小值，数据类型和因素列中的级别数。
    
    请考虑在进行任何类型的数据输入、功能转换或功能工程后运行此函数。 通过这样做，你可以确保所有你想要使用您的模型中的功能的所需的数据类型和避免出错。
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **结果**
    
    ```
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

2. 现在，调用 RevoScaleR 函数[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)以获取有关单个变量的详细统计信息。

    rxSummary 基于 R`summary`起作用，但具有一些其他功能和优点。 rxSummary 在多个计算上下文中工作，并支持分块。  你还可以使用 rxSummary 来转换值，或汇总基于因素级别。
    
    在此示例中，你可以汇总票费量基于乘客数目。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一个参数指定公式或其他词语进行汇总方式。 在这里，`F()`函数用于将转换中的值_乘客\_计数_到之前汇总的因素。 此外必须为指定的最小值 (1) 和最大值 (6)_乘客\_计数_因素变量。
    + 如果未指定输出的统计信息，默认情况下 rxSummary 输出平均值、 StDev、 Min、 Max 和有效且缺少观测值的数目。
    + 本示例中也包括跟踪函数开始时间和完成时间的代码，以便可以比较性能。
  
    **结果**

    如果成功运行 rxSummary 函数，你应看到类似这样，结果按类别跟统计信息列表。 

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>对大数据的好处是可以练习

请尝试定义的所有行的新查询字符串。 我们建议你设置此试验新数据源对象。 你还可能尝试更改*rowsToRead*参数，以查看它如何影响吞吐量。

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
> 在此运行时，你可以使用之类的工具[进程资源管理器](https://technet.microsoft.com/sysinternals/processexplorer.aspx)或使用 SQL Server 服务运行 SQL 事件探查器以查看如何建立连接和 R 代码。
> 
> 另一个选项是监视在使用这些 SQL Server 上运行的 R 作业[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="next-lesson"></a>下一课

[使用 R 创建图形和绘图](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>上一课

[使用 SQL 探索数据](walkthrough-view-and-explore-the-data.md)
