---
title: "定义并使用计算上下文（对数据科学的深入探讨）| Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a682a40a9a62af3e1ff18ec0cc777ac9c1da7a9e
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="define-and-use-compute-contexts"></a>定义并使用计算上下文


假设你想要在服务器上（而不是本地计算机上）执行一些更复杂的计算。 为此，可以创建计算上下文，让 R 代码在服务器上运行。

**RxInSqlServer** 函数是 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 包中提供的增强型 R 函数之一。 该函数处理以下任务：创建数据库连接，在本地计算机和远程执行上下文之间传递对象。

在此步骤中，将学习如何使用 **RxInSqlServer** 函数在 R 代码中定义计算上下文。

若要创建计算上下文，则需要以下与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关的基本信息：

- 实例的连接字符串
- 输出处理方式的规范
- 用于启用跟踪或指定共享目录的可选参数

## <a name="create-and-set-a-compute-context"></a>创建并设置计算上下文

1. 为将执行计算的实例指定连接字符串。  这仅是为创建计算上下文而传递到 *RxInSqlServer* 函数的几个变量之一。 可以重复使用以前创建的连接字符串，或者创建一个不同的连接字符串（如果想要将计算移到另一个服务器或想要使用不同的标识）。

    **使用 SQL 登录名**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **使用 Windows 身份验证**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. 指定所需的输出处理方式。 在以下代码中，你要指出工作站上的 R 会话应始终等待 R 作业结果，但不从远程计算返回控制台输出。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    到 RxInSqlServer 的 wait 参数支持以下选项：
  
    -   **TRUE**。 作业将为阻塞性且不会返回，直到它已完成或失败。  有关详细信息，请参阅[分布式和 Microsoft R 中的并行计算](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。
  
    -   **FALSE**。 作业将为非阻塞性且会立即返回，你可以继续运行其他 R 代码。 但是，即使在非阻塞模式下，作业运行时，也必须维持客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接。

3. 或者，可以指定本地 R 会话与远程  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机及其帐户共享使用的本地目录的位置。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 如果你想要手动创建共享的特定目录，则可以添加如下所示的行。 若要确定哪个文件夹当前正在使用的共享，请运行`rxGetComputeContext`，这将返回有关当前的详细信息计算上下文。 有关详细信息，请参阅 [ScaleR 参考](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver)。

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 具有准备好所有变量，让他们为 RxInSqlServer 构造函数来创建的变量*计算上下文对象*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    你可能会发现 RxInSqlServer * 的语法是与你之前用来定义数据源的 RxSqlServerData 函数几乎完全相同。 但是，它们之间存在以下重要差异。
      
    - 通过使用函数 RxSqlServerData，定义的数据源对象指定数据的存储位置。
    
    - 与此相反，（通过使用函数 RxInSqlServer 定义） 的计算上下文指示聚合和其他计算所在做好准备。
    
    定义计算上下文不会影响任何其他可能在工作站上执行的泛型 R 计算，也不会更改数据源。 例如，你可以将本地文本文件定义为数据源，但会将计算上下文更改为 SQL Server 并对 SQL Server 计算机上的数据执行所有的读取和汇总操作。

## <a name="enable-tracing-on-the-compute-context"></a>在计算上下文上启用跟踪

有时操作在本地上下文中正常工作，但在远程计算上下文中运行时会有问题。 如果想要分析问题或监视性能，则可以在计算上下文中启用跟踪，支持运行时的疑难解答。

1. 创建新的计算上下文，使用相同的连接字符串，但添加参数*traceEnabled*和*traceLevel*到*RxInSqlServer*构造函数。

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
    在此示例中，将 *traceLevel* 属性设置为 7，这意味着“显示所有跟踪信息”。

2. 若要更改计算上下文，请使用 rxSetComputeContext 函数，并按名称指定的上下文。

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 在本教程中，我们将使用未启用跟踪的计算上下文。 这是因为尚未经过启用跟踪的选项的性能测试的所有操作。
    > 
    > 但是，如果你决定使用跟踪，请注意您的体验可能会受网络连接中的一种。

现在已创建了远程计算上下文，你将学习如何更改计算上下文，以便在服务器上或本地运行 R 代码。

## <a name="next-step"></a>下一步

[创建和运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>上一步

[查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)


