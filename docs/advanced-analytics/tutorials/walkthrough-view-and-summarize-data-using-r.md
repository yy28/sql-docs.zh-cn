---
title: 使用 R 函数查看和汇总 SQL Server 数据
description: 本教程演示如何使用 R 函数对 SQL Server 上的数据库内分析可视化和生成统计摘要。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 52ba1a8f036037ade42c8483b1735c84cc72867e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345782"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>使用 R 查看和汇总 SQL Server 数据 (演练)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程介绍**RevoScaleR**包中的函数, 并指导你完成以下任务:

> [!div class="checklist"]
> * 连接到 SQL Server
> * 定义具有所需数据的查询或指定表或视图
> * 定义当运行 R 代码时要使用的一个或多个计算上下文
> * (可选) 定义在从源读取数据源时应用于该数据源的转换

## <a name="define-a-sql-server-compute-context"></a>定义 SQL Server 计算上下文

在客户端工作站上的 R 环境中运行以下 R 语句。 本部分假设有[Microsoft R Client 的数据科学工作站](../r/set-up-a-data-science-client.md), 因为它包括所有 RevoScaleR 包以及一组基本的轻型 R 工具。 例如, 你可以使用 Rgui.exe 来运行本部分中的 R 脚本。

1. 如果尚未加载**RevoScaleR**包, 请运行以下 R 代码行:

    ```R
    library("RevoScaleR")
    ```

     引号是可选的, 在这种情况下, 建议使用引号。
     
     如果遇到错误, 请确保 R 开发环境使用的库包括 RevoScaleR 包。 使用命令 (如) `.libPaths()`查看当前库路径。

2. 为 SQL Server 创建连接字符串, 并将其保存在 R 变量*connStr*中。

   必须将占位符 "your_server_name" 更改为有效的 SQL Server 实例名称。 对于服务器名称, 你可能只能使用实例名称, 或者可能需要完全限定名称, 具体取决于你的网络。
    
   对于 SQL Server 身份验证, 连接语法如下:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    对于 Windows 身份验证, 语法稍有不同:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    通常, 我们建议尽可能使用 Windows 身份验证, 以避免在 R 代码中保存密码。

3. 定义用于创建新*计算上下文*的变量。 创建计算上下文对象后, 可以使用它在 SQL Server 实例上运行 R 代码。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机之间来回序列化 R 对象时，R 会使用临时目录。 可指定用作 sqlShareDir  的本地目录，或者接受默认目录。
  
    - 使用*sqlWait*指示您是否希望 R 等待来自服务器的结果。  有关等待作业与非等待作业的讨论, 请参阅[使用 Microsoft R 中的 RevoScaleR 进行分布式和并行计算](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用参数*sqlConsoleOutput*指示不需要查看 R 控制台的输出。

4. 调用[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)构造函数来创建具有已定义的变量和连接字符串的计算上下文对象, 并将新对象保存在 R 变量*sqlcc 中*中。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 默认情况下, 计算上下文是本地的, 因此需要显式设置*活动*计算上下文。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)返回前面的活动计算上下文, 以便可以使用它
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)返回活动计算上下文
    
    请注意, 设置计算上下文只会影响使用**RevoScaleR**包中的函数的操作;计算上下文不会影响执行开源 R 操作的方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>使用 RxSqlServer 创建数据源

使用 RevoScaleR 和 MicrosoftML 之类的 Microsoft R 库时,*数据源*是使用 RevoScaleR 函数创建的对象。 数据源对象指定要用于任务的一组数据, 如模型定型或功能提取。 可以从各种源 (包括 SQL Server) 获取数据。 有关当前支持的源的列表, 请参阅[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

之前, 您定义了一个连接字符串, 并将该信息保存在 R 变量中。 您可以重复使用该连接信息来指定要获取的数据。

1. 将 SQL 查询另存为字符串变量。 查询定义用于定型模型的数据。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我们在此处使用了 TOP 子句来使任务运行得更快, 但根据顺序, 查询返回的实际行可能会有所不同。 因此, 您的汇总结果也可能与下面列出的结果不同。 随意删除 TOP 子句。

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
    
    + colClasses   参数指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 间移动数据时要使用的列类型。这一点非常主要，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的数据类型不同于 R，且使用的数据类型更多。 有关详细信息, 请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。
  
    + 参数*rowsPerRead*对于管理内存使用情况和高效计算非常重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中大多数增强的分析函数都可以处理区块中的数据并累积中间结果，并在读取所有的数据后返回最终的计算。  通过添加*rowsPerRead*参数, 您可以控制将多少行数据读入每个块区以便进行处理。  如果此参数的值太大, 数据访问速度可能会很慢, 因为没有足够的内存来有效处理此类大型数据块。  在某些系统中, 将*rowsPerRead*设置为过小的值还可以提供较慢的性能。

3. 此时, 您已创建了*inDataSource*对象, 但它不包含任何数据。 在运行[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)等函数之前, 不会将数据从 SQL 查询提取到本地环境。

    不过, 现在您已经定义了数据对象, 您可以将其用作其他函数的参数。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 R 摘要中的 SQL Server 数据

在本部分中, 你将尝试中[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的几个支持远程计算上下文的函数。 通过将 R 函数应用到数据源, 您可以浏览、汇总和绘制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据图表。

1. 调用函数[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)可获取数据源中的变量列表及其数据类型。

    **rxGetVarInfo**是一种便捷的功能;您可以对任何数据帧或远程数据对象中的数据集调用此方法, 以获取最大值和最小值、数据类型和因子列中的级别数等信息。
    
    请考虑在进行任何类型的数据输入、功能转换或功能工程后运行此函数。 这样, 就可以确保要在模型中使用的所有功能都是预期的数据类型, 并避免错误。
  
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

2. 现在, 调用 RevoScaleR 函数[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) , 获取有关各个变量的详细统计信息。

    rxSummary 基于 R `summary`函数, 但具有一些额外的功能和优势。 rxSummary 在多个计算上下文中工作, 支持分块。  您还可以使用 rxSummary 来转换值或基于系数级别进行汇总。
    
    在此示例中, 将基于乘客的数量汇总费用金额。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一个参数指定汇总的公式或字词。 在此, `F()`函数用于在汇总前将_乘客\_计数_中的值转换为一些因素。 还必须为_乘客\_计数_系数变量指定最小值 (1) 和最大值 (6)。
    + 如果未指定要输出的统计信息, 则默认情况下, rxSummary 将输出均值、StDev、Min、Max 和有效和缺失的观察值。
    + 本示例中也包括跟踪函数开始时间和完成时间的代码，以便可以比较性能。
  
    **结果**

    如果 rxSummary 函数成功运行, 则应看到如下所示的结果, 然后是按类别列出的统计信息列表。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>大数据的额外练习

尝试使用所有行定义新的查询字符串。 建议为此试验设置新的数据源对象。 你还可以尝试更改*rowsToRead*参数以查看它如何影响吞吐量。

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
> 在此过程中运行时, 可以使用[进程资源管理](https://technet.microsoft.com/sysinternals/processexplorer.aspx)器或 SQL 事件探查器等工具来查看如何建立连接, 以及如何使用 SQL Server 服务运行 R 代码。
> 
> 另一种选择是使用这些[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)监视 SQL Server 上运行的 R 作业。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 创建图形和绘图](walkthrough-create-graphs-and-plots-using-r.md)