---
title: "定义和使用计算上下文 （SQL 和 R 深入） |Microsoft 文档"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3db63204c3c2e904d2e4a8ba3fa8087bcfdbb1f5
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>定义和使用计算上下文 （SQL 和 R 深入）

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

本课程介绍[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函数，这样就可以为 SQL Server 定义计算上下文，然后在服务器上，而不是本地计算机上执行复杂计算。 

RevoScaleR 支持多个计算上下文，以便你可以在 Hadoop、 Spark 中或数据库中运行 R 代码。 对于 SQL Server，你定义的服务器，并函数处理的任务的创建本地计算机和远程执行上下文之间的连接和传递对象的数据库。

创建 SQL Server 的函数计算上下文使用的以下信息：

- 连接字符串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例
- 应如何处理输出的规范
- 启用跟踪，或指定跟踪级别的可选参数
- 共享的数据目录的可选规范

## <a name="create-and-set-a-compute-context"></a>创建并设置计算上下文

1. 指定在其中执行计算实例的连接字符串。  你可以重新使用之前创建的连接字符串。 如果你想要将计算移动到不同的服务器，或使用不同的登录名执行某些任务，你可以创建不同的连接字符串。

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
  
    -   **TRUE**。 作业配置为阻止，并且不返回直到它已完成或失败。  有关详细信息，请参阅[分布式和机器学习 Server 中的并行计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**。 作业配置为非阻塞，并立即返回，允许你继续运行其他 R 代码。 但是，即使在非阻塞模式下，作业运行时，也必须维持客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接。

3. 或者，可以指定用于本地 R 会话进行的远程共享的本地目录的位置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机和其帐户。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 如果你想要手动创建共享的特定目录，你可以添加类似于以下行：

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    若要确定哪个文件夹当前正在使用的共享，请运行`rxGetComputeContext()`，这将返回有关当前的详细信息计算上下文。 有关详细信息，请参阅 [ScaleR 参考](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/)。

4. 具有准备好所有变量，作为自变量提供这些**RxInSqlServer**构造函数，来创建*计算上下文对象*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    语法**RxInSqlServer**看起来几乎与的**RxSqlServerData**你之前用来定义数据源的函数。 但是，它们之间存在以下重要差异。
      
    - 使用函数 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 定义的数据源对象指定数据的存储位置。
    
    - 计算上下文中，通过使用函数的定义与此相反， [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)指示聚合和其他计算所在做好准备。
    
    定义计算上下文不会影响任何其他可能在工作站上执行的泛型 R 计算，也不会更改数据源。 例如，你可以将本地文本文件定义为数据源，但会将计算上下文更改为 SQL Server 并对 SQL Server 计算机上的数据执行所有的读取和汇总操作。

## <a name="enable-tracing-on-the-compute-context"></a>在计算上下文上启用跟踪

有时操作在本地上下文中正常工作，但在远程计算上下文中运行时会有问题。 如果想要分析问题或监视性能，则可以在计算上下文中启用跟踪，支持运行时的疑难解答。

1. 创建新的计算上下文，使用相同的连接字符串，但添加参数*traceEnabled*和*traceLevel*到**RxInSqlServer**构造函数。

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

2. 若要更改计算上下文，请使用 [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 函数，并按名称指定上下文。

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 对于本教程，使用没有启用的跟踪的计算上下文。 
    > 
    > 但是，如果你决定使用跟踪，请注意您的体验可能会受网络连接中的一种。 另请注意，因为尚未经过启用跟踪的选项的性能测试的所有操作。

了解如何使用的下一步计算上下文中，若要运行的服务器上的 R 代码或本地。

## <a name="next-step"></a>下一步

[创建并运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>上一步

[查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
