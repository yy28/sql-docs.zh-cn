---
title: "要开始使用 Docker 上的 SQL Server 2017 |Microsoft 文档"
description: "此快速入门教程演示如何使用 Docker 运行 SQL Server 2017 容器映像。 然后创建并查询使用 sqlcmd 数据库。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: 10623562f57ae1b4b571dd2e5b7dad56b81b8f8b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>使用 Docker 运行 SQL Server 2017 容器映像

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在本快速入门教程，你使用 Docker 以拉取和运行 SQL Server 自 2017 年 1 RC2 容器映像， [mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)。 然后通过连接**sqlcmd**创建第一个数据库和运行查询。

此映像包含在 Linux（基于 Ubuntu 16.04）上运行的 SQL Server。 它可与适用于 Linux 的 Docker 引擎 1.8 以上版本或适用于 Mac/Windows 的 Docker 配合使用。

> [!NOTE]
> 本快速入门专门重点介绍使用 mssql server linux 映像。 未涵盖的 Windows 映像，但你可以了解有关它在[mssql server windows Docker Hub 页](https://hub.docker.com/r/microsoft/mssql-server-windows/)。

## <a id="requirements"></a> 先决条件

- 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。
- 至少 4 GB 的磁盘空间
- 至少 4 GB 的 RAM
- [在 Linux 上的 SQL Server 的系统需求](sql-server-linux-setup.md#system)。

> [!IMPORTANT]
> Docker for Mac 和 Docker for Windows 的 Moby VM 默认大小为 2 GB，因此必须将其更改为 4 GB。 如果你在 Mac 或 Windows 上运行，请使用以下过程来增加内存。

### <a name="increase-docker-memory-to-4-gb-mac"></a>Docker 将内存增加为 4 GB (Mac)

以下步骤适用于为 4 GB 的 Mac for Docker 增加内存。

1. 单击顶部状态栏上的 Docker 徽标。
1. 选择**首选项**。
1. 将内存指示器移到 4 GB 或以上。
1. 单击**重新启动**在屏幕的按钮的按钮。

### <a name="increase-docker-memory-to-4-gb-windows"></a>Docker 将内存增加为 4 GB (Windows)

以下步骤来增加为用于 Windows 的 Docker 为 4 GB 内存。

1. 右键单击任务栏中的 Docker 图标。
1. 单击**设置**该菜单下。
1. 单击**高级**选项卡。
1. 将内存指示器移到 4 GB 或以上。
1. 单击**应用**按钮。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

1. 从 Docker 中心请求容器映像。

    ```bash
    docker pull microsoft/mssql-server-linux
    ```

    > [!TIP]
    > 对于 Linux，具体取决于您系统和用户的配置，你可能需要开头每`docker`命令`sudo`。

    > [!NOTE]
    > 上面的命令中提取最新的 SQL Server 容器映像。 如果你想要请求的特定映像，则添加冒号和标记名称 (例如， `microsoft/mssql-server-linux:rc1`)。 若要查看所有可用映像，请参阅[mssql server linux Docker 中心页](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

1. 若要使用 Docker 运行容器映像，可以使用以下命令从 bash shell (Linux/macOS):

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    如果你使用的用于 Windows 的 Docker，使用提升的 PowerShell 命令的提示符中的以下命令：

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    > [!NOTE]
    > Bash (Linux/macOS) 示例和 PowerShell (Windows) 示例的唯一区别是单引号与双-用括号括起来的环境变量。 如果你使用错误的一个，docker run 命令将失败。 本主题的其余部分，为方便起见提供 bash 和 PowerShell 代码块。 如果只有一个示例，它将适用于所有平台，包括 Windows。

    下表提供了参数在前面的说明`docker run`示例：

    | 参数 | Description |
    |-----|-----|
    | **-e ACCEPT_EULA = Y** |  设置**ACCEPT_EULA**变量为任何值，以确认你接受[最终用户许可协议](http://go.microsoft.com/fwlink/?LinkId=746388)。 SQL Server 映像的必需设置。 |
    | **-e MSSQL_SA_PASSWORD =\<YourStrong ！Passw0rd\>** | 指定你自己的强密码至少 8 个字符并达到[SQL 服务器的密码要求](../relational-databases/security/password-policy.md)。 SQL Server 映像的必需设置。 |
    | **-e MSSQL_PID = 开发人员** | 指定的版本或产品密钥。 在此示例中，随意许可的开发人员版适用于非生产测试。 其他值，请参阅[与环境变量在 Linux 上配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。 |
    | **-cap 添加 SYS_PTRACE** | 增加了 Linux 功能来跟踪进程。 这使 SQL Server 生成转储在出现异常。 |
    | **-p 1401:1433** | 建立主机环境（第一个值）上的 TCP 端口与容器（第二个值）中 TCP 端口的映射。 在此示例中，SQL Server 侦听 TCP 1433 容器中，并且这公开给端口 1401，主机上。 |
    | **microsoft/mssql-服务器的 linux** | SQL Server Linux 容器映像。 除非另行指定，则默认为**最新**映像。 |

1. 若要查看你的 Docker 容器，请使用`docker ps`命令。

    ```bash
    docker ps -a
    ```

    将看到与如下屏幕截图相似的输出：

    ![Docker ps 命令输出](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. 如果**状态**列显示的状态**向上**，然后在容器中运行 SQL Server 且在侦听端口指定**端口**列。 如果**状态**你 SQL 服务器容器显示的列**Exited**，请参阅[故障排除部分中的配置指南](sql-server-linux-configure-docker.md#troubleshooting)。

有两个有用`docker run`不使用在前面的示例为简单起见选项。 `-h` （主机名） 参数更改为自定义值的容器的内部名称。 这是你将看到以下 TRANSACT-SQL 查询中返回的名称：

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

你还可能会发现`--name`有用命名你的容器，而不是拥有生成的容器名称的参数。 设置`-h`和`--name`为相同的值是一种好方法，可以轻松地识别目标容器。

## <a name="change-the-sa-password"></a>更改 SA 密码

SA 帐户是在安装过程中创建的 SQL Server 实例上的系统管理员。 创建 SQL Server 容器之后,`MSSQL_SA_PASSWORD`你指定的环境变量是可发现的通过运行`echo $MSSQL_SA_PASSWORD`容器中。 出于安全考虑，更改 SA 密码。

1. 选择要使用 SA 用户的强密码。

1. 使用`docker exec`运行**sqlcmd**若要使用 TRANSACT-SQL 更改密码。 替换`<Old Password>`和`<New Password>`替换为您的密码值。

> ```bash
> docker exec -it <Container ID> /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<Old Password>' -Q 'ALTER LOGIN SA WITH PASSWORD="<New Password>";'
> ```

## <a name="connect-to-sql-server"></a>连接到 SQL Server

下列步骤将使用 SQL Server 命令行工具， **sqlcmd**，要连接到 SQL Server 的容器内。

1. 使用`docker exec -it`命令来启动交互式 bash shell 内你正在运行的容器。 在下面的示例`e69e056c702d`是容器 id。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 无需始终指定完整的容器 ID。只需要指定足够的字符，能够唯一标识它即可。 在此示例中，它可能是足够用于`e6`或`e69`而不是完整的 id。

1. 一旦位于容器内部，使用 sqlcmd 进行本地连接。 Sqlcmd 不在默认情况下，路径因此你必须指定完整路径。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

   > [!TIP]
   > 可以省略命令行上提示要输入的密码。

1. 如果成功，应会显示 sqlcmd 命令提示符：`1>`。

## <a name="create-and-query-data"></a>创建和查询数据

以下部分将引导你使用 sqlcmd 和 Transact-SQL 完成新建数据库、添加数据并运行简单查询的整个过程。

### <a name="create-a-new-database"></a>新建数据库

以下步骤创建一个名为 `TestDB` 的新数据库。

1. 在 sqlcmd 命令提示符中，粘贴以下 Transact-SQL 命令以创建测试数据库：

   ```sql
   CREATE DATABASE TestDB
   ```

1. 在下一行中，编写一个查询以返回服务器上所有数据库的名称：

   ```sql
   SELECT Name from sys.Databases
   ```

1. 前两个命令没有立即执行。 必须在新行中键入 `GO` 才能执行以前的命令：

   ```sql
   GO
   ```

### <a name="insert-data"></a>插入数据

接下来创建一个新表 `Inventory`，然后插入两个新行。

1. 在 sqlcmd 命令提示符中，将上下文切换到新的 `TestDB` 数据库：

   ```sql
   USE TestDB
   ```

1. 创建名为 `Inventory` 的新表：

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 将数据插入新表：

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. 要执行上述命令的类型 `GO`：

   ```sql
   GO
   ```

### <a name="select-data"></a>选择数据

现在，运行查询以从 `Inventory` 表返回数据。

1. 通过 sqlcmd 命令提示符输入查询，以返回 `Inventory` 表中数量大于 152 的行：

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 执行命令：

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>退出 sqlcmd 命令提示符

1. 要结束 sqlcmd 会话，请键入 `QUIT`：

   ```sql
   QUIT
   ```

1. 若要退出容器中的交互式命令提示，请键入`exit`。 退出交互式 Bash Shell 后，容器将继续运行。

## <a name="connect-from-outside-the-container"></a>从连接容器之外

你可以还连接到 SQL Server 实例在 Docker 上从任何外部的 Linux、 Windows 或 macOS 工具支持 SQL 连接。

以下步骤使用**sqlcmd**外部容器连接到在容器中运行的 SQL Server。 这些步骤假定你已在你的容器之外安装的 SQL Server 命令行工具。 相同的主体应用时使用其他工具，但连接的过程是唯一的每个工具。

1. 查找承载你的容器的计算机的 IP 地址。 在 Linux 上，使用**ifconfig**或**ip addr**。在 Windows 上，使用**ipconfig**。

1. 运行指定的 IP 地址和端口映射到容器中的端口 1433年的 sqlcmd。 在此示例中，这是端口 1401年主机计算机上。

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
   ```

1. 运行 TRANSACT-SQL 命令。 完成后，键入`QUIT`。

若要连接到 SQL Server 其他常见工具包括：

- [Visual Studio 代码](sql-server-linux-develop-use-vscode.md)
- [在 Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>后续步骤

若要浏览其他方案，例如正在运行的多个容器，数据持久性和故障排除，请参阅[Docker 上的配置 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)。

此外，请查看[mssql docker GitHub 存储库](https://github.com/Microsoft/mssql-docker)对资源、 反馈和已知的问题。

