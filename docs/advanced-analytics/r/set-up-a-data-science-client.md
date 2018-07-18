---
title: 设置 SQL Server 上的 R 开发数据科学客户端 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dd0b420630846382b9d7cf456352bb606a4f0040
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204559"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>设置 SQL Server 上的 R 开发数据科学客户端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

配置的实例后[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]若要支持机器学习，应设置可以连接到远程执行和部署服务器的开发环境。

本指南介绍了一些典型的客户端方案，包括免费的 Visual Studio 社区版，以在 SQL Server 中运行 R 代码的配置。

## <a name="install-r-libraries-on-the-client"></a>在客户端上安装 R 库

客户端环境必须包括 Microsoft R Open，以及支持在 SQL Server 上分布式执行 R 的其他 RevoScaleR 包。 标准分发的 R 不具有支持远程计算上下文或并行执行 R 任务的包。

若要获取这些库，请安装以下任一项：
  
+ [Microsoft R Client](http://aka.ms/rclient/download)

+ Microsoft R Server (for SQL Server 2016)

    - 若要从 SQL Server 安装程序安装，请参阅[安装 SQL Server 2016 R Server （独立）](../install/sql-r-standalone-windows-install.md)

    - 若要使用单独的基于 Windows 的安装程序，请参阅[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ 机器学习服务器 （用于 SQL Server 自 2017 年)

    - 若要从 SQL Server 安装程序安装，请参阅[安装 SQL Server 自 2017 年 1 机器学习服务器 （独立）](../install/sql-machine-learning-standalone-windows-install.md)

    - 若要使用单独的基于 Windows 的安装程序，请参阅[适用于 Windows 中安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="r-tools"></a>R 工具

当与 SQL Server 安装 R 时，可以使用任何安装的相同 R 工具**基**R，如 RGui、 Rterm，等的安装。 因此从技术上讲，你具有所需开发和测试 R 代码的所有工具。

以下标准 R 工具都将纳入*基本安装*，因此默认情况下安装。

+ **RTerm**： 用于运行 R 脚本的命令行终端

+ **RGui.exe**：适用于 R 的简单交互式编辑器。RGui.exe 和 RTerm 的命令行参数相同。

+ **RScript**：用于以批处理模式运行 R 脚本的命令行工具。

若要找到这些工具，确定设置 SQL Server 或独立机器学习功能一起安装的 R 库。 例如，在默认安装中，R 工具位于以下文件夹：

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 独立： `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 自 2017 年 1 机器学习服务： `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 机器学习 Server （独立）： `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

如果你需要使用 R 工具的帮助，只需打开**RGui**，单击**帮助**，然后选择其中一个选项

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R 客户端是一个免费下载，使你可以访问的开发使用 RevoScaleR 包。 通过安装 R 客户端，你可以创建可以在所有受支持的计算上下文，包括 SQL Server 数据库中分析和分布式 R 计算 Hadoop、 Spark 中或使用机器学习服务器的 Linux 上运行的 R 解决方案。

如果你已安装不同的 R 开发环境，如 RStudio，一定要重新配置要使用的库和可执行文件由 Microsoft R 客户端提供的环境。 通过这样你可以使用 RevoScaleR 包的所有功能尽管性能将受到限制。

有关详细信息，请参阅[什么是 Microsoft R 客户端？](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="install-a-development-environment"></a>安装开发环境

如果你还没有首选的 R 开发环境，我们建议以下项之一：

+ 用于 Visual Studio 的 R 工具

    与 Visual Studio 2015 一起使用。

    安装程序信息，请参阅[如何安装 R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。
 
    若要配置 RTVS 为使用你的 Microsoft R 客户端库，请参阅[有关 Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    即使是免费的社区版包括数据科学工作负荷，安装适用于 R、 Python 和 F # 的项目模板。

    下载 Visual Studio 中，从[此站点](https://www.visualstudio.com/vs/)。 

+ RStudio

    如果你偏好使用 RStudio，需要执行一些附加的步骤来使用 RevoScaleR 库：

    - 安装 Microsoft R 客户端，以获得所需的包和库。
    - 更新你的 R 路径以使用 Microsoft R 运行时。

    有关详细信息，请参阅[R 客户端-配置您的 IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide)。

## <a name="configure-your-ide"></a>配置 IDE

+ 用于 Visual Studio 的 R 工具

    请参阅[此站点](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)有关如何生成和调试 R 的一些示例项目使用 R Tools for Visual Studio。 

+ Visual Studio 2017

    如果你安装 Microsoft R 客户端或 R Server**之前**安装 Visual Studio、 R Server 库自动检测和用于你的库路径。 如果你不安装 RevoScaleR 库中，从**R 工具**菜单上，选择**安装 R 客户端**。

## <a name="run-r-in-sql-server"></a>在 SQL Server 中运行 R

此示例使用 Visual Studio 2017 Community Edition，其安装数据科学工作负荷。

1. 从**文件**菜单上，选择**新建**，然后选择**项目**。

2. -手工窗格包含预安装的模板的列表。 单击**R**，然后选择**的 R 项目**。 在**名称**框中，键入`dbtest`单击**确定**。

3. Visual Studio 将创建一个新的项目文件夹和默认脚本文件中， `Script.R`。 

4. 类型`.libPaths()`脚本的第一行上文件，，然后按 CTRL + enter 键。

5. 当前的 R 库路径应显示在**R 交互式**窗口。 

6. 单击**R 工具**菜单，然后选择**Windows**以查看其他 R 特定窗口，你可以在工作区中显示的列表。
 
    + 通过按 CTRL + 3，查看当前存储库中的包的帮助。
    + 请参阅中的 R 变量**变量资源管理器**，通过按 CTRL + 8。

7. 创建 SQL Server 实例的连接字符串和 RxInSqlServer 构造函数中使用的连接字符串创建一个 SQL Server 数据源对象。 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```

    > [!TIP]
    > 若要运行一批，选择你想要运行，按 CTRL + enter 键的行。

8. 到服务器，设置计算上下文，然后对数据运行一些简单的 R 代码。

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    返回结果的顺序**R 交互式**窗口。
    
    如果你想要确保自己的 SQL Server 实例上执行的代码，你可以使用探查器创建跟踪。