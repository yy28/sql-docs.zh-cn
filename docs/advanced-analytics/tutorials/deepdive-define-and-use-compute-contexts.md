---
title: 定义和使用 RevoScaleR 计算上下文
description: 有关如何在 SQL Server 上使用 R 语言定义计算上下文的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5fb28af293c549a9f5494ab08c6c01ebf5d2a20
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715547"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>定义并使用计算上下文 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在上一课中, 你使用**RevoScaleR**函数来检查数据对象。 本课程介绍[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函数, 该函数使你可以为远程 SQL Server 定义计算上下文。 使用远程计算上下文, 你可以将 R 执行从本地会话转移到服务器上的远程会话。 

> [!div class="checklist"]
> * 了解远程 SQL Server 计算上下文的元素
> * 在计算上下文对象上启用跟踪

**RevoScaleR**支持多个计算上下文:Hadoop、Spark 上的 Spark, 以及数据库中的 SQL Server。 对于 SQL Server, **RxInSqlServer**函数用于服务器连接, 并在本地计算机和远程执行上下文之间传递对象。

## <a name="create-and-set-a-compute-context"></a>创建和设置计算上下文

创建 SQL Server 计算上下文的**RxInSqlServer**函数使用以下信息:

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接字符串
+ 应如何处理输出的规范
+ 共享数据目录的可选规范
+ 启用跟踪或指定跟踪级别的可选参数

本部分将指导你完成每个部分。

1. 为执行计算的实例指定连接字符串。 你可以重新使用之前创建的连接字符串。

    **使用 SQL 登录名**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **使用 Windows 身份验证**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 指定所需的输出处理方式。 以下脚本将引导本地 R 会话在处理下一个操作之前在服务器上等待 R 作业结果。 它还会禁止在本地会话中显示远程计算的输出。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    到 RxInSqlServer 的 wait 参数支持以下选项：
  
    -   **TRUE**。 作业配置为 "阻止", 并且在完成或失败之前不会返回。  有关详细信息, 请参阅[Machine Learning Server 中的分布式计算和并行计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**。 作业配置为非阻塞并立即返回, 使你可以继续运行其他 R 代码。 但是，即使在非阻塞模式下，作业运行时，也必须维持客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接。

3. (可选) 指定本地 R 会话以及远程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机及其帐户共享使用的本地目录的位置。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   如果要手动创建用于共享的特定目录, 可以添加一行, 如下所示:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 将自变量传递给**RxInSqlServer**构造函数以创建*计算上下文对象*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    **RxInSqlServer**的语法看起来与之前用于定义数据源的**RxSqlServerData**函数的语法几乎相同。 但是，它们之间存在以下重要差异。
      
    - 使用函数 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 定义的数据源对象指定数据的存储位置。
    
    - 相反, 计算上下文 (使用函数[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)定义) 指示聚合和其他计算发生的位置。
    
    定义计算上下文不会影响任何其他可能在工作站上执行的泛型 R 计算，也不会更改数据源。 例如，你可以将本地文本文件定义为数据源，但会将计算上下文更改为 SQL Server 并对 SQL Server 计算机上的数据执行所有的读取和汇总操作。

5. 激活远程计算上下文。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 返回有关计算上下文的信息, 包括其属性。

    ```R
    rxGetComputeContext()
    ```

7. 通过指定 "local" 关键字将计算上下文重置回本地计算机 (下一课将演示如何使用远程计算上下文)。

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 有关此函数支持的其他关键字的列表，请从 R 命令行键入 `help("rxSetComputeContext")` 。

## <a name="enable-tracing"></a>启用跟踪

有时操作在本地上下文中正常工作，但在远程计算上下文中运行时会有问题。 如果要分析问题或监视性能, 可以在计算上下文中启用跟踪, 以支持运行时故障排除。

1. 创建使用同一连接字符串的新计算上下文, 但将参数*traceEnabled*和*TraceLevel*添加到**RxInSqlServer**构造函数。

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

2. 使用[rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)函数按名称指定启用跟踪的计算上下文。

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>后续步骤

了解如何切换计算上下文以在服务器上或在本地运行 R 代码。

> [!div class="nextstepaction"]
> [本地和远程计算上下文中的计算汇总统计信息](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)