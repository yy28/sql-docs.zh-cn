---
title: "要开始使用 Docker 上的 SQL Server 2017 |Microsoft 文档"
description: "本快速入门演示如何使用 Docker 运行 SQL Server 2017 容器映像。 然后创建并查询使用 sqlcmd 数据库。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: 1f018dd2b60365d89e912e7ef38499f8a4d14d9b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>使用 Docker 运行 SQL Server 2017 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门教程，你使用 Docker 以拉取和运行 SQL Server 2017 容器映像， [mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)。 然后通过连接**sqlcmd**创建第一个数据库和运行查询。

此映像包含在 Linux（基于 Ubuntu 16.04）上运行的 SQL Server。 它可与适用于 Linux 的 Docker 引擎 1.8 以上版本或适用于 Mac/Windows 的 Docker 配合使用。

> [!NOTE]
> 本快速入门专门重点介绍使用 mssql-服务器-**linux**映像。 未涵盖的 Windows 映像，但你可以了解有关它在[mssql server 的 windows 开发人员 Docker Hub 页](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)。

## <a id="requirements"></a> 先决条件

- 适用于支持的任一 Linux 分发版的 Docker 引擎 1.8 以上版本，或适用于 Mac/Windows 的 Docker。 有关详细信息，请参阅[安装 Docker](https://docs.docker.com/engine/installation/)。
- 至少 2 GB 的磁盘空间
- 至少 2 GB 的 RAM
- [在 Linux 上的 SQL Server 的系统需求](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

1. 从 Docker Hub 中拉出 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   前一个命令中提取最新的 SQL Server 2017 容器映像。 如果你想要请求的特定映像，则添加冒号和标记名称 (例如， `microsoft/mssql-server-linux:2017-GA`)。 若要查看所有可用映像，请参阅[mssql server linux Docker 中心页](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

1. 若要使用 Docker 运行容器映像，可以使用以下命令从 bash shell (Linux/macOS) 或提升的 PowerShell 命令提示符。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > 密码应遵循 SQL Server 默认密码策略，否则为该容器不可以安装 SQL server，并将停止工作。 默认情况下，密码必须是至少 8 个字符且包含以下四个集的三类字符： 大写字母、 小写字母，以 10 为基数数字和符号。 你可以通过执行检查错误日志[docker 日志](https://docs.docker.com/engine/reference/commandline/logs/)命令。

   > [!NOTE]
   > 默认情况下，这将创建一个容器的 SQL Server 2017 开发人员版。 在容器中运行生产版本的过程是略有不同。 有关详细信息，请参阅[运行容器映像的生产](sql-server-linux-configure-docker.md#production)。

   下表提供了参数在前面的说明`docker run`示例：

   | 参数 | Description |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  设置**ACCEPT_EULA**变量为任何值，以确认你接受[最终用户许可协议](http://go.microsoft.com/fwlink/?LinkId=746388)。 SQL Server 映像的必需设置。 |
   | **-e 'MSSQL_SA_PASSWORD=\<YourStrong!Passw0rd\>'** | 指定你自己的强密码至少 8 个字符并达到[SQL Server 密码要求](../relational-databases/security/password-policy.md)。 SQL Server 映像的必需设置。 |
   | **-p 1401:1433** | 建立主机环境（第一个值）上的 TCP 端口与容器（第二个值）中 TCP 端口的映射。 在此示例中，SQL Server 侦听 TCP 1433 容器中，并且这公开给端口 1401，主机上。 |
   | **--name sql1** | 指定容器，而不是一个随机生成的自定义名称。 如果你运行多个容器，你无法重用此相同的名称。 |
   | **microsoft/mssql-server-linux:2017-latest** | SQL Server 2017 Linux 容器映像。 |

1. 若要查看你的 Docker 容器，请使用`docker ps`命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   将看到与如下屏幕截图相似的输出：

   ![Docker ps 命令输出](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. 如果**状态**列显示的状态**向上**，然后在容器中运行 SQL Server 且在侦听端口指定**端口**列。 如果**状态**你 SQL 服务器容器显示的列**Exited**，请参阅[故障排除部分中的配置指南](sql-server-linux-configure-docker.md#troubleshooting)。

`-h` （主机名） 参数也非常有用，但不是使用在本教程中为简单起见，它。 这会容器的内部名称更改为自定义值。 这是你将看到以下 TRANSACT-SQL 查询中返回的名称：

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

设置`-h`和`--name`为相同的值是一种好方法，可以轻松地识别目标容器。

## <a name="change-the-sa-password"></a>更改 SA 密码

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>连接到 SQL Server

下列步骤将使用 SQL Server 命令行工具， **sqlcmd**，要连接到 SQL Server 的容器内。

1. 使用`docker exec -it`命令来启动交互式 bash shell 内你正在运行的容器。 在下面的示例`sql1`由指定名称`--name`参数创建容器时。

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. 一旦位于容器内部，使用 sqlcmd 进行本地连接。 Sqlcmd 不在默认情况下，路径因此你必须指定完整路径。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
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

## <a id="connectexternal"></a> 从连接容器之外

你可以还连接到 SQL Server 实例在 Docker 上从任何外部的 Linux、 Windows 或 macOS 工具支持 SQL 连接。

以下步骤使用**sqlcmd**外部容器连接到在容器中运行的 SQL Server。 这些步骤假定你已在你的容器之外安装的 SQL Server 命令行工具。 相同的主体应用时使用其他工具，但连接的过程是唯一的每个工具。

1. 查找承载你的容器的计算机的 IP 地址。 在 Linux 上，使用**ifconfig**或**ip addr**。在 Windows 上，使用**ipconfig**。

1. 运行指定的 IP 地址和端口映射到容器中的端口 1433年的 sqlcmd。 在此示例中，这是端口 1401年主机计算机上。

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. 运行 TRANSACT-SQL 命令。 完成后，键入`QUIT`。

若要连接到 SQL Server 其他常见工具包括：

- [Visual Studio 代码](sql-server-linux-develop-use-vscode.md)
- [在 Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)
- [SQL Server 操作 Studio （预览版）](../sql-operations-studio/what-is.md)
- [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>删除容器

如果你想要删除 SQL Server 容器使用在本教程中，运行以下命令：

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 停止并永久删除容器中删除容器中的任何 SQL Server 数据。 如果你需要以保留数据，[创建并复制出的容器的备份文件](tutorial-restore-backup-in-sql-server-container.md)或使用[容器数据持久性技术](sql-server-linux-configure-docker.md#persist)。

## <a name="docker-demo"></a>Docker 演示

你尝试对 Docker 使用 SQL Server 容器映像后，你可能想要知道如何使用 Docker 来提高开发和测试。 下面的视频演示如何在持续集成和部署方案中使用 Docker。

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>后续步骤

有关如何将数据库备份文件还原到容器的教程，请参阅[Linux Docker 容器中的 SQL Server 数据库还原](tutorial-restore-backup-in-sql-server-container.md)。 若要浏览其他方案，例如正在运行的多个容器，数据持久性和故障排除，请参阅[Docker 上的配置 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)。

此外，请查看[mssql docker GitHub 存储库](https://github.com/Microsoft/mssql-docker)对资源、 反馈和已知的问题。
