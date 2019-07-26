---
title: 使用 RevoScaleR rxExec 在 SQL Server 上运行自定义 R 函数
description: 有关如何使用 RevoScaleR 函数在 SQL Server 上运行自定义 R 脚本的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d90e2d4887154d3545884a77d0290e632f04a569
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470601"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>使用 rxExec 在 SQL Server 上运行自定义 R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

你可以通过[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)传递函数在 SQL Server 上下文中运行自定义 R 函数, 假设你的脚本所需的所有库也安装在服务器上, 而这些库与 R 的基本分发兼容。 

**RevoScaleR**中的**rxExec**函数提供了一种机制, 用于运行所需的任何 R 脚本。 此外, **rxExec**可以在单个服务器中的多个内核之间显式分发工作, 将 "扩展" 添加到仅限于本机 R 引擎的资源约束的脚本。

在本教程中, 你将使用模拟数据来演示在远程服务器上运行的自定义 R 函数的执行。

## <a name="prerequisites"></a>先决条件

+ [SQL Server 2017 机器学习服务 (带 R)](../install/sql-machine-learning-services-windows-install.md)或[SQL Server 2016 R Services (数据库内)](../install/sql-r-services-windows-install.md)
  
+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录

+ [具有 RevoScaleR 库的开发工作站](../r/set-up-a-data-science-client.md)

客户端工作站上的 R 分发版提供内置的**rgui.exe**工具, 可用于在本教程中运行 R 脚本。 还可以使用 IDE, 例如 RStudio 或针对 Visual Studio 的 R 工具。

## <a name="create-the-remote-compute-context"></a>创建远程计算上下文

在客户端工作站上运行以下 R 命令。 例如, 你使用的是**rgui.exe**, 请从以下位置启动它:C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 为执行计算的 SQL Server 实例指定连接字符串。 服务器必须配置为 R 集成。 此练习中不使用数据库名称, 但连接字符串需要一个名称。 如果有测试或示例数据库, 则可以使用该数据库。

    **使用 SQL 登录名**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **使用 Windows 身份验证**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 为连接字符串中引用的 SQL Server 实例创建远程计算上下文。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 激活计算上下文, 然后将对象定义返回为确认步骤。 应会看到计算上下文对象的属性。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>创建自定义函数

在此练习中, 您将创建一个自定义 R 函数, 该函数模拟包含一对骰子的常见 casino。 游戏规则确定赢或丢失结果:

+ 在初始滚动时滚动7或11。
+ 滚动2、3或12将丢失。
+ 滚动4、5、6、8、9或 10, 则该数字将成为你的点, 并继续滚动, 直到再次滚动你的点 (在这种情况下, 你会获胜) 或滚动 7 (在这种情况下, 你会丢失)。

通过创建自定义函数，然后多次运行该函数便可轻松在 R 中模拟此游戏。

1.  使用以下 R 代码创建自定义函数：
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  通过运行函数模拟单条骰子游戏。
  
    ```R
    rollDice()
    ```
  
    你是胜了还是败了？
  
现在, 你已创建了一个操作脚本, 接下来让我们了解如何使用**rxExec**多次运行该函数, 以创建可帮助确定赢率的模拟。

## <a name="pass-rolldice-in-rxexec"></a>在 rxExec 中传递 rollDice ()

若要在远程 SQL Server 的上下文中运行任意函数, 请调用**rxExec**函数。

1. 调用自定义函数作为**rxExec**的参数, 以及修改模拟的其他参数。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + 使用 timesToRun 参数，指示执行函数的次数。  在这种情况下，将掷 20 次骰子。
  
    + 可使用 RNGseed 和 RNGkind 参数控制随机数的生成。 将 RNGseed 设置为“自动”时，会在每个辅助角色上初始化并行随机数流。
  
2. rxExec 函数会创建一个列表，其中一次运行一个元素；但是，在列表完成前，不会看到太多操作执行。 所有迭代完成后, 以**length**开头的行将返回一个值。
  
    然后可以转到下一步，获得输赢记录的汇总。
  
3. 使用 R 的 unlist 函数将返回的列表转换为向量，并使用 table 函数汇总结果。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    结果应如下所示：
  
     *成功丢失* *12 8*

## <a name="conclusion"></a>结束语

虽然这种做法很简单, 但它演示了在 SQL Server 上运行的 R 脚本中集成任意 R 函数的重要机制。 总结实现此方法的关键点:

+ 必须为机器学习和 R 集成配置 SQL Server:[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)r 功能, 或[SQL Server 2016 R Services (数据库内)](../install/sql-r-services-windows-install.md)。

+ 函数中使用的开源或第三方库 (包括任何依赖项) 必须安装在 SQL Server 上。 有关更多信息，请参阅[安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。

+ 将脚本从开发环境转移到强化的生产环境可能会导致防火墙和网络限制。 请仔细测试, 确保脚本能够按预期执行。

## <a name="next-steps"></a>后续步骤

有关使用**rxExec**的更复杂示例, 请参阅以下文章:[通过 foreach 和 rxExec 进行粗粒度并行](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
