---
title: "使用 R 查看和汇总数据（数据科学端到端演练） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 查看和汇总数据（数据科学端到端演练）
现在使用 R 代码处理相同的数据。 还将介绍如何使用随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 附带的 **RevoScaleR** 包中的函数在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器的上下文中生成数据摘要，并将结果发送回 R 环境。  

本演练提供的 R 脚本包括创建数据对象、生成摘要和生成模型所需的所有代码。 R 脚本文件 **RSQL_RWalkthrough.R**位于脚本文件的安装位置。  
+ 如果熟悉 R，则可同时运行所有脚本。
+ 对于 RevoScaleR 初学者，本教程会逐行指导此脚本
+ 若要运行此脚本中的各个行，可突出显示文件中的行，然后按 Ctrl + Enter。    
  
> [!TIP]  保存 R 工作区，以防你想要稍后完成本演练的剩余部分。  通过这种方式，数据对象和其他变量可供重新使用。   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>定义 SQL Server 数据源和计算上下文
若要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 获取 R 代码中要使用的数据，则需要：  
  
- 创建与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接  
- 定义具有所需数据的查询或指定表或视图    
- =定义运行 R 代码时要使用的一个或多个计算上下文    
-   （可选）定义可应用于数据源的函数  
 

### <a name="load-the-revoscaler-library"></a>加载 RevoScaleR 库

+  如果 **RevoScaleR** 包未加载，请运行：
    ```R
    library("RevoScaleR")`.  
    ```  
    如果遇到错误，请确保你的 R 开发环境使用的是包括 RevoScaleR 软件包的库。 使用命令（例如，`.libPaths())`）查看当前路径：  

    如果这是首次使用 **RevoScaleR** 包，可以键入 `help("RevoScaleR")` 或 `help("RxSqlServerData")` 在 R 环境中获取联机帮助。  

### <a name="create-connection-strings"></a>创建连接字符串


1. 定义连接字符串。 对于本演练，我们提供了 SQL 登录名和 Windows 集成身份验证两个示例。 我们推荐尽可能使用 Windows 身份验证，以避免在 R 代码中保存密码。

    使用的帐户必须具有在指定数据库中读取数据和创建新表的权限。 有关如何将用户添加到 SQL 数据库并为他们提供正确的权限的信息，请参阅[安装后服务器配置 (SQL Server R Services)](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md)。 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] 请确保根据需要编辑服务器名称、数据库名称、用户名和密码。 
      
  
### <a name="define-and-set-a-compute-context"></a>定义并设置计算上下文  

接下来，定义一个可使 R 代码在 SQL Server 计算机上运行的计算上下文。 通常情况下，当使用 R 时，将在计算机的内存中运行所有操作。 但是，通过指示 R 操作应在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上运行，可并行运行部分任务和利用服务器资源。  

默认情况下，计算上下文位于本地，因而需显式设置计算上下文，具体取决于操作。  


1.  首先定义一些用于创建计算上下文的变量。  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机之间来回序列化 R 对象时，R 会使用临时目录。 可指定用作 sqlShareDir 的本地目录，或者接受默认目录。  
  
    -   使用 sqlWait 指示是否要 R 等待结果。  有关等待作业与非等待作业的讨论，请参阅 [ScaleR 分布式计算](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。
  
    -   使用 sqlConsoleOutput 参数指示不需显示 R 控制台的输出。  
  
2.  创建已定义变量和连接字符串的计算上下文对象，并将其保存在 R 变量 sqlcc 中。  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. 设置计算上下文。
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + `rxSetComputeContext` 会无形返回先前活动的计算上下文，使其可供使用
   + `rxGetComputeContext` 返回活动的计算上下文  
  
    请注意，设置计算上下文仅影响使用 **RevoScaleR** 包中的函数的操作；该计算上下文不会影响开源代码 R 操作的执行方式。  
  
### <a name="create-an-rxsqlserver-data-object"></a>创建 RxSqlServer 数据对象  

定义要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接后，可将数据连接对象用作基础来定义不同的数据源。 数据源指定了要用于任务（例如定型、探索、计分和生成功能）的某些数据集。  
    
通过使用 RxSqlServer 函数并传递连接字符串和要获取的数据定义来定义 SQL Server 集。  
  
1. 将 SQL 语句保存为字符串变量。 此查询定义用来定型模型的数据。    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. 将查询定义作为参数传递到 SQL Server 数据源。 通过映射 SQL，colClasses参数指定要返回数据的架构 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + colClasses 参数指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 间移动数据时要使用的列类型。这一点非常主要，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的数据类型不同于 R，且使用的数据类型更多。 有关详细信息，请参阅[使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)。  
  
    + rowsPerRead 参数对于处理内存使用率和高效计算非常重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中大多数增强的分析函数都可以处理区块中的数据并累积中间结果，并在读取所有的数据后返回最终的计算。  通过添加 `rowsPerRead` 参数，可以控制每个区块读取的数据行数，以进行处理。  如果此参数的值太大，则数据访问可能很慢，因为没有足够的内存来有效地处理如此大型的数据区块。  在某些系统中，将 `rowsPerRead` 的值设置得过小也可能使性能下降。  

> [!TIP] 创建 inDataSource 对象后，可以根据需要重复使用此对象，以获取有关数据和所使用的变量的基本信息、操作和转换数据，或者用于为模型定型。  但是，目前 inDataSource 对象自身尚不包含 SQL 查询中的任何数据。 运行参数（例如 rxImport 或 rxSummary）时数据才会被提取到本地环境中。          
  
## <a name="using-the-sql-server-data-in-r"></a>在 R 中使用 SQL Server 数据  
现在可以将 R 函数应用到数据源，以浏览、总结和绘制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。 在此部分中，你将尝试 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中提供的几个支持远程计算上下文的函数。  
  
-   `rxGetVarInfo`：对远程数据对象中的任何数据帧或数据集（也包括部分列表和矩阵）使用此函数，以获取最大值和最小值、数据类型和因子列中的级别数等信息。  
  
    请考虑在进行任何类型的数据输入、功能转换或功能工程后运行此函数。 这样做可以确保你想要在模型中使用的所有功能都为预期的数据类型，并避免错误。  
 
  
-   `rxSummary`：使用此函数获取有关各个变量的详细统计信息。 此外还可以转换值，使用因素级别计算摘要并保存摘要以便重复使用。  
  
  
### <a name="inspect-variables-in-the-data-source"></a>检查数据源中的变量  
    
+ 使用数据源 `rxGetVarInfo`作为参数调用函数  `inDataSource` ，以获取数据源中的变量列表及其数据类型。  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    结果：  
  变量 1：tipped，类型：整型  **  
  变量 2：fare_amount，类型：数值型  **  
  变量 3：passenger_count，类型：整型  **  
  变量 4：trip_time_in_secs，类型：数值型，存储：int64  **  
  变量 5：trip_distance，类型：数值型  **  
  变量 6：pickup_datetime，类型：字符型  **  
  变量 7：dropoff_datetime，类型：字符型  **  
  变量 8：pickup_longitude，类型：数值型  **  
  变量 9：pickup_latitude，类型：数值型  **  
  变量 10：dropoff_longitude，类型：数值型  **  
  
### <a name="create-a-summary-using-r"></a>使用 R 创建摘要

+ 基于乘客数量，调用 RevoScaleR 函数 `rxSummary` 汇总票费金额。 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + 第一个 `rxSummary` 参数指定汇总的公式或字词。 此处，使用 `F()` 函数在汇总前将 passenger_count 中的值转换为因子。  
    + 如果未指定要输出的统计信息， `rxSummary` 默认输出 Mean、StDev、Min、Max 和有效且缺失的观察值。  
    + 本示例中也包括跟踪函数开始时间和完成时间的代码，以便可以比较性能。  
  
    结果  
  rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)  **  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
  Number of valid observations: 1000  **   
  Name                          Mean    StdDev   Min Max ValidObs MissingObs  **  
  fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0  **   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>下一步  
[使用 R 创建图形和绘图（数据科学端到端演练）](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
