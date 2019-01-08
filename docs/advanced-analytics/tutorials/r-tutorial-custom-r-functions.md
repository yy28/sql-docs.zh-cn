---
title: 使用 RevoScaleR rxExec 的 SQL Server 机器学习的 SQL Server 上运行自定义 R 函数
description: 有关如何使用 RevoScaleR 函数的 SQL Server 上运行自定义 R 脚本的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 90790c2b96843ea1821b8b4ed05052a7611cdf74
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596438"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>使用 rxExec 的 SQL Server 上运行自定义 R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

可以通过传递通过函数的 SQL Server 的上下文中运行自定义 R 函数[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)，假设您的脚本需要的所有库还会在服务器上都安装和这些库与基兼容分发的。 

**RxExec**函数，在**RevoScaleR**提供了用于运行所需的任何 R 脚本的机制。 此外， **rxExec**能够工作显式分布在一台服务器，将缩放添加到否则仅限于本机 R 引擎的资源约束的脚本中的多个内核。

在本教程中，您将使用模拟的数据来演示在远程服务器运行的自定义 R 函数的执行。

## <a name="prerequisites"></a>先决条件

+ [（使用 R) SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)或[SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)
  
+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录名

+ [通过 RevoScaleR 库的开发工作站](../r/set-up-a-data-science-client.md)

客户端工作站上的 R 分布提供了内置**Rgui**工具，可以使用在本教程中运行 R 脚本。 用于 Visual Studio 中，还可以使用 RStudio 或 R 工具等 IDE。

## <a name="create-the-remote-compute-context"></a>创建远程计算上下文

客户端工作站上运行下面的 R 命令。 例如，使用**Rgui**，从此位置开始：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 指定在其中执行计算的 SQL Server 实例的连接字符串。 服务器必须配置为 R 集成。 在此练习中，不使用的数据库名称，但连接字符串需要一个。 如果有测试或示例数据库，可以使用的。

    **使用 SQL 登录名**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **使用 Windows 身份验证**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 创建到 SQL Server 实例的连接字符串中引用的远程计算上下文。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 激活计算上下文，并返回一个确认步骤形式的对象定义。 应看到计算上下文对象的属性。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>创建自定义函数

在此练习中，将创建一个模拟常见的赌场组成枚骰子的自定义 R 函数。 游戏的规则确定了 win 或丢失的结果：

+ 次掷 7 或 11，您就赢。
+ 回滚 2，3，或 12，则会丢失。
+ 4、 5、 6、 8、 9、 或 10，则该点数成为你的点，并且继续掷，直至你可以部署点再次 (win 这种情况下) 或播广告 7，在这种情况下您会丢失。

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
  
2.  通过运行该函数可模拟单个掷骰子游戏。
  
    ```R
    rollDice()
    ```
  
    你是胜了还是败了？
  
现在，已有的操作的脚本，让我们了解如何使用**rxExec**运行函数多次创建有助于确定获胜概率的模拟。

## <a name="pass-rolldice-in-rxexec"></a>传入 rxExec rollDice()

若要在远程 SQL 服务器的上下文中运行任意函数，调用**rxExec**函数。

1. 自定义函数作为参数调用**rxExec**一起修改模拟其他参数。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + 使用 timesToRun 参数，指示执行函数的次数。  在这种情况下，将掷 20 次骰子。
  
    + 可使用 RNGseed 和 RNGkind 参数控制随机数的生成。 将 RNGseed 设置为“自动”时，会在每个辅助角色上初始化并行随机数流。
  
2. rxExec 函数会创建一个列表，其中一次运行一个元素；但是，在列表完成前，不会看到太多操作执行。 当所有迭代都都完成时，使用开头的行**长度**将返回一个值。
  
    然后可以转到下一步，获得输赢记录的汇总。
  
3. 使用 R 的 unlist 函数将返回的列表转换为向量，并使用 table 函数汇总结果。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    结果应如下所示：
  
     *败胜* *12 8*

## <a name="conclusion"></a>结束语

尽管此练习是过于简单，但它演示了一种重要机制集成在 SQL Server 上运行的 R 脚本中的任意 R 函数。 若要汇总的关键点，以便此方法：

+ 必须针对机器学习和 R 集成配置 SQL Server:[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)与 R 功能或[SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)。

+ SQL Server 上必须安装在函数中，包括任何依赖项，使用的开放源代码或第三方库。 有关更多信息，请参阅[安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。

+ 将脚本从开发环境移到强化的生产环境可能会引入防火墙和网络限制。 仔细测试以确保您的脚本是能够按预期方式执行。

## <a name="next-steps"></a>后续步骤

有关使用的更复杂示例**rxExec**，请参阅以下文章：[使用 foreach 和 rxExec 粗粒度并行度](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
