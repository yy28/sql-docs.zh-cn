---
title: "定义并使用计算上下文（对数据科学的深入探讨） | Microsoft Docs"
ms.custom: ""
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 定义并使用计算上下文（对数据科学的深入探讨）
已决定在服务器上，而不是本地计算机上执行一些更复杂的计算。 若要执行此操作，必须创建允许在服务器上运行 R 代码的计算上下文。  
  
[RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver) 函数是 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 包中提供的增强型 R 函数之一。 该函数处理以下任务：创建数据库连接，在本地计算机和远程执行上下文之间传递对象。  
  
在此步骤中，将学习如何使用 *RxInSqlServer* 函数在 R 代码中定义计算上下文。  


  
## 创建并设置计算上下文  
若要创建计算上下文，则需要以下与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关的基本信息：  
  
-   实例的连接字符串  
-   输出处理方式的规范  
-   用于启用跟踪或指定共享目录的可选参数


 现在开始操作。

1.  为将执行计算的实例指定连接字符串。  这仅是为创建计算上下文而传递到 *RxInSqlServer* 函数的几个变量之一。 

    **使用 SQL 登录名**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **使用集成的 Windows 身份验证**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  指定所需的输出处理方式。 在以下代码中，你要指出工作站上的 R 会话应始终等待 R 作业结果，但不从远程计算返回控制台输出。  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    到 RxInSqlServer 的 wait 参数支持以下选项：  
  
    -   **TRUE**。 作业将为阻塞性且不会返回，直到它已完成或失败。  有关阻塞性和非阻塞性作业的详细信息，请参阅 
  
    -   **FALSE**。 作业将为非阻塞性且会立即返回，你可以继续运行其他 R 代码。 但是，即使在非阻塞模式下，作业运行时，也必须维持客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接。  

3. 或者，可以指定本地 R 会话与远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机及其帐户共享使用的本地目录的位置。
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    建议使用默认值，而不用手动指定此参数的文件夹。 有关详细信息，请参阅 [ScaleR 参考](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver)。
    
    如果你仅想了解正在使用的文件夹，则可以运行 `rxGetComputeContext` 来查看有关当前计算机上下文的详细信息。 
  

4.  准备好所有变量后，将它们作为参数提供给 `RxInSqlServer` 构造函数来定义计算上下文对象。  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    你可能会看到 RxInSqlServer 的语法几乎与你之前用来定义数据源的 RxSqlServerData 函数的语法相同。 但是，它们之间存在以下重要差异。  
  
    -   使用函数 RxSqlServerData 定义的数据源对象指定数据的存储位置。  
  
    -   与之相反，计算上下文（使用函数 RxInSqlServer 定义）指示聚合和其他计算发生的位置。  
  
    定义计算上下文不会影响任何其他可能在工作站上执行的泛型 R 计算，也不会更改数据源。 例如，你可以将本地文本文件定义为数据源，但会将计算上下文更改为 SQL Server 并对 SQL Server 计算机上的数据执行所有的读取和汇总操作。 
  
## 在计算上下文上启用跟踪  
在特定的远程计算上下文中运行时，对本地上下文的操作有时会遇到问题。 如果想要分析问题或监视性能，则可以在计算上下文中启用跟踪，支持运行时的疑难解答。  
  
1. 创建使用相同连接字符串的新计算上下文，但将参数 traceEnabled 和 traceLevel 添加到 RxInSqlServer 构造函数。  
  
    ```R  
    sqlComputeTrace <- RxInSqlServer(   
        connectionString = sqlConnString,        
        #shareDir = sqlShareDir,  
        wait = sqlWait,   
        consoleOutput = sqlConsoleOutput,       
        traceEnabled = TRUE,
        traceLevel = 7)  
    ```  
  
    在此示例中，将 traceLevel 的属性设置为 7，这意味着“显示所有跟踪信息”  

2. 若要随时切换到此计算上下文，请使用 rxSetComputeContext 函数，并按名称指定上下文。

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    在本教程中，我们将使用未启用跟踪的计算上下文。 启用跟踪选项的性能尚未针对所有操作进行测试，你的体验可能因网络连接而有所不同。  
  
现在已创建了远程计算上下文，你将学习如何更改计算上下文，以便在服务器上或本地运行 R 代码。  
  
## 下一步  
[第 2 课：创建和运行 R 脚本（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## 上一步  
[查询和修改 SQL Server 数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## 另请参阅  
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
