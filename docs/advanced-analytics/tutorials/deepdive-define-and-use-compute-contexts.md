---
title: 定义并使用 RevoScaleR 计算上下文的 SQL Server 机器学习
description: 有关如何定义计算上下文在 SQL Server 上使用 R 语言的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3131dfc65d8964232073d37aba697f62de9fcc2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962231"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>定义和使用计算上下文 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在上一课中，您使用**RevoScaleR**函数来检查数据的对象。 本课将介绍[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函数，它允许您定义的 SQL Server 的远程计算上下文。 使用远程计算上下文，你可以在服务器上上移到远程会话的 R 执行本地会话中。 

> [!div class="checklist"]
> * 了解远程 SQL Server 中的元素计算上下文
> * 在计算上下文对象上启用跟踪

**RevoScaleR**支持多个计算上下文：Hadoop、 Spark on HDFS 和 SQL Server 数据库中。 对于 SQL Server， **RxInSqlServer**函数用于服务器连接和本地计算机和远程执行上下文之间传递对象。

## <a name="create-and-set-a-compute-context"></a>创建并设置计算上下文

**RxInSqlServer**创建 SQL Server 计算上下文的函数使用以下信息：

+ 连接字符串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例
+ 应如何处理输出的规范
+ 共享的数据目录的可选规范
+ 启用跟踪或指定跟踪级别的可选参数

此部分将指导你完成每个部分。

1. 指定在其中执行计算的实例的连接字符串。 您可以重新使用之前创建的连接字符串。

    **使用 SQL 登录名**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **使用 Windows 身份验证**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 指定所需的输出处理方式。 以下脚本将定向本地 R 会话之前要等待 R 作业结果在服务器上处理下一步操作。 它还将阻止从远程计算使其不显示本地会话的输出。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    到 RxInSqlServer  的 wait  参数支持以下选项：
  
    -   **TRUE**。 该作业配置为阻止并不会返回直到它已完成或失败。  有关详细信息，请参阅[分布式计算和机器学习服务器中的并行计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**。 作业配置为非阻塞，并立即返回，你可以继续运行其他 R 代码。 但是，即使在非阻塞模式下，作业运行时，也必须维持客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接。

3. （可选） 指定用于通过本地 R 会话与远程共享的本地目录的位置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机和其帐户。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   如果你想要手动创建共享的特定目录，则可以添加行如下所示：

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 将参数传递给**RxInSqlServer**构造函数创建*计算上下文对象*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    语法**RxInSqlServer**看起来几乎与**RxSqlServerData**你之前用来定义数据源的函数。 但是，它们之间存在以下重要差异。
      
    - 使用函数 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 定义的数据源对象指定数据的存储位置。
    
    - 与此相反，计算上下文中，使用定义的函数[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)指示聚合和其他计算发生。
    
    定义计算上下文不会影响任何其他可能在工作站上执行的泛型 R 计算，也不会更改数据源。 例如，你可以将本地文本文件定义为数据源，但会将计算上下文更改为 SQL Server 并对 SQL Server 计算机上的数据执行所有的读取和汇总操作。

5. 激活远程计算上下文。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 返回有关计算上下文，包括其属性的信息。

    ```R
    rxGetComputeContext()
    ```

7. 通过指定"local"（下一课演示如何使用远程计算上下文） 关键字将计算上下文重置回本地计算机。

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 有关此函数支持的其他关键字的列表，请从 R 命令行键入 `help("rxSetComputeContext")` 。

## <a name="enable-tracing"></a>启用跟踪

有时操作在本地上下文中正常工作，但在远程计算上下文中运行时会有问题。 如果你想要分析问题或监视性能，可以启用跟踪在计算上下文中，以支持运行时进行故障排除。

1. 创建新的计算上下文，使用相同的连接字符串，但添加参数*traceEnabled*并*traceLevel*到**RxInSqlServer**构造函数。

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

2. 使用[rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)函数按名称指定启用了跟踪的计算上下文。

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>后续步骤

了解如何切换计算上下文来运行 R 代码在服务器上的或本地。

> [!div class="nextstepaction"]
> [计算摘要统计信息在本地和远程计算上下文](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)