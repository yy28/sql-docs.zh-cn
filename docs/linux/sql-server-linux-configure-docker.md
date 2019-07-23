---
title: Docker 上的 SQL Server 的配置选项
description: 探索在 Docker 中使用和与 SQL Server 2017 和2019预览版容器映像交互的不同方式。 这包括保存数据、复制文件和故障排除。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388382"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上配置 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何使用 Docker 配置和使用[mssql-server linux 容器映像](https://hub.docker.com/_/microsoft-mssql-server)。 此映像包含在 Linux（基于 Ubuntu 16.04）上运行的 SQL Server。 它可与适用于 Linux 的 Docker 引擎 1.8 以上版本或适用于 Mac/Windows 的 Docker 配合使用。

> [!NOTE]
> 本文专门介绍如何使用 mssql-server-linux 映像。 Windows 映像未涵盖, 但你可以在[mssql-server-Windows Docker Hub 页面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)上了解有关该映像的详细信息。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

若要拉取并运行 SQL Server 2017 和 SQL Server 2019 preview 的 Docker 容器映像, 请按照以下快速入门中的先决条件和步骤进行操作:

- [通过 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md?view=sql-server-2017)
- [通过 Docker 运行 SQL Server 2019 预览容器映像](quickstart-install-connect-docker.md?view=sql-server-ver15)

此配置文章提供了以下部分中的其他使用方案。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>运行基于 RHEL 的容器映像

SQL Server Linux 容器映像上的所有文档都指向基于 Ubuntu 的容器。 从 SQL Server 2019 preview 开始, 你可以使用基于 Red Hat Enterprise Linux (RHEL) 的容器。 在所有 docker 命令中, 将容器存储库从**mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu**更改为**mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1** 。

例如, 以下命令将拉取使用 RHEL 的最新 SQL Server 2019 预览版容器:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>运行生产容器映像

上一节中的快速入门将从 Docker Hub 运行免费的 Developer edition SQL Server。 如果要运行生产容器映像 (如 Enterprise、Standard 或 Web 版本), 则大多数信息仍适用。 不过, 这里列出了几个差异。

- 如果具有有效的许可证, 则只能在生产环境中使用 SQL Server。 可在[此处](https://go.microsoft.com/fwlink/?linkid=857693)获取免费的 SQL Server Express 生产许可证。 SQL Server Standard 和 Enterprise Edition 许可证均可通过[Microsoft 批量许可](https://www.microsoft.com/licensing/default.aspx)获得。


- 开发人员容器映像也可以配置为运行生产版。 使用以下步骤来运行生产版:

查看[快速入门](quickstart-install-connect-docker.md)中的要求和运行过程。 必须用**MSSQL_PID**环境变量指定生产版本。 下面的示例演示如何运行企业版最新的 SQL Server 2017 容器映像:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> 通过将值**Y**传递到环境变量**ACCEPT_EULA** , 并将版本值传递到**MSSQL_PID**, 你会表达你具有要使用的版本和版本 SQL Server 的有效现有许可证。 你还同意你对 Docker 容器映像中运行的 SQL Server 软件的使用受 SQL Server 许可证条款的约束。

> [!NOTE]
> 有关**MSSQL_PID**的可能值的完整列表, 请参阅[使用 Linux 上的环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

::: moniker-end

## <a name="connect-and-query"></a>连接和查询

可以从容器外部或内部对容器中的 SQL Server 进行连接和查询。 以下各节介绍了这两种方案。 

### <a name="tools-outside-the-container"></a>容器外的工具

可以从支持 SQL 连接的任何 Linux、Windows 或 macOS 外部工具连接到 Docker 计算机上的 SQL Server 实例。 一些常用工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [适用于 Windows 的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

下面的示例使用**sqlcmd**连接到在 Docker 容器中运行的 SQL Server。 连接字符串中的 IP 地址是运行容器的主机的 IP 地址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果映射的主机端口不是默认的**1433**, 请将该端口添加到连接字符串。 例如, 如果`docker run`在命令中`-p 1400:1433`指定了, 则通过显式指定端口1400进行连接。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器内的工具

从 SQL Server 2017 preview 开始, [SQL Server 的命令行工具](sql-server-linux-setup-tools.md)包含在容器映像中。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

1. 使用 `docker exec -it` 命令在运行的容器内部启动交互式 Bash Shell。 在下面的示例`e69e056c702d`中, 为容器 ID。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 无需始终指定完整的容器 ID。只需要指定足够的字符，能够唯一标识它即可。 在此示例中, 可以使用`e6`或`e69`而不是完整的 id。

2. 一旦位于容器内部，使用 sqlcmd 进行本地连接。 请注意， 默认情况下，sqlcmd 不在路径之中，因此需要指定完整的路径。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 完成 sqlcmd 后, 键入`exit`。

4. 完成交互式命令提示后, 键入`exit`。 退出交互式 Bash Shell 后，容器将继续运行。

## <a name="run-multiple-sql-server-containers"></a>运行多个 SQL Server 容器

Docker 支持在同一主机上运行多个 SQL Server 容器。 这就为要求在同一主机上运行多个 SQL Server 实例的方案提供了解决办法。 每个容器必须在一个不同的端口上公开自身。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

以下示例创建两个 SQL Server 2017 容器, 并将其映射到主机上的端口**1401**和**1402** 。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

以下示例创建两个 SQL Server 2019 预览容器, 并将其映射到主机上的端口**1401**和**1402** 。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

现在，两个 SQL Server 实例在单独的容器内运行。 客户端可通过使用 Docker 主机的 IP 地址和容器的端口号连接每个 SQL Server 实例。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>创建自定义容器

可以创建自己的[Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) , 以创建自定义 SQL Server 容器。 有关详细信息, 请参阅[结合 SQL Server 和 Node 应用程序的演示](https://github.com/twright-msft/mssql-node-docker-demo-app)。 如果创建自己的 Dockerfile, 请注意前台进程, 因为此过程控制容器的生命周期。 如果它退出, 容器将关闭。 例如, 如果想要运行脚本并开始 SQL Server, 请确保 SQL Server 进程是最适合的命令。 所有其他命令都在后台运行。 Dockerfile 中的以下命令演示了这一点:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果你反转了上一示例中的命令, 则在 do-my-sql-commands.sh 脚本完成时, 容器将关闭。

## <a id="persist"></a>保留数据

即使你用`docker stop`和`docker start`重新启动容器, 你的 SQL Server 配置更改和数据库文件也会保留在容器中。 但是, 如果删除容器`docker rm`, 则会删除容器中的所有内容, 包括 SQL Server 和数据库。 以下部分介绍如何使用**数据卷**来持久保存数据库文件, 即使关联的容器已被删除。

> [!IMPORTANT]
> 就 SQL Server 而言，了解 Docker 中的数据持久性至关重要。 除了本部分中的讨论, 请参阅 Docker 的文档, 了解[如何在 docker 容器中管理数据](https://docs.docker.com/engine/tutorials/dockervolumes/)。

### <a name="mount-a-host-directory-as-data-volume"></a>将主机目录装载为数据卷

第一种方法是在主机上装载目录，将其作为容器中的数据卷。 为此, 请将`docker run`命令`-v <host directory>:/var/opt/mssql`与标志一起使用。 这允许在容器执行之间还原数据。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

通过此方法，还能共享和查看位于主机上、Docker 外的文件。

> [!IMPORTANT]
> 当前不支持 Mac 上的 Docker 与 Linux 映像上 SQL Server 的主机卷映射。 请改为使用数据卷容器。 此限制特定于`/var/opt/mssql`目录。 从已装载目录进行读取操作可正常运行。 例如, 可以在 Mac 上使用-v 装载主机目录, 并从驻留在主机上的 .bak 文件还原备份。

### <a name="use-data-volume-containers"></a>使用数据卷容器

第二个方法是使用数据卷容器。 可以通过使用`-v`参数指定卷名而不是主机目录来创建数据卷容器。 以下示例创建名为**sqlvolume**的共享数据卷。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> 早期版本的 Docker 不支持通过此方法在 run 命令中隐式创建数据卷。 在这种情况下, 请使用 Docker 文档中概述的显式步骤,[创建和装入数据卷容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)。

即使停止并删除此容器，数据卷仍然存在。 您可以通过`docker volume ls`命令查看它。

```bash
docker volume ls
```

如果稍后又创建了另一个具有相同卷名的容器，则这个新容器将使用卷中包含的相同 SQL Server 数据。

若要删除数据卷容器, 请使用`docker volume rm`命令。

> [!WARNING]
> 如果删除数据卷容器, 则会*永久*删除该容器中的任何 SQL Server 数据。

### <a name="backup-and-restore"></a>备份和还原

除这些容器技术外，还可使用 SQL Server 标准备份和还原技术。 可通过备份文件来保护数据，或将数据移动至其他 SQL Server 实例。 有关详细信息, 请参阅[在 Linux 上备份和还原 SQL Server 数据库](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如要创建备份，请确保在容器外部创建或复制备份文件。 否则，一旦删除容器，也将随之删除备份文件。

## <a name="execute-commands-in-a-container"></a>在容器中执行命令

如果正在运行容器，那么可以从主机终端在容器内部执行命令。

要获取容器 ID，请运行：

```bash
docker ps
```

要在容器中启动 Bash 终端，请运行：

```bash
docker exec -it <Container ID> /bin/bash
```

现在，可以运行这些命令，就像在容器内的终端上运行那样。 完成后，键入 `exit`。 这将退出交互式命令会话，但容器将继续运行。

## <a name="copy-files-from-a-container"></a>从容器复制文件

要从容器复制文件，请使用下列命令：

```bash
docker cp <Container ID>:<Container path> <host path>
```

**示例：**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>将文件复制到容器中

要将文件复制到容器中，请使用下列命令：

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**示例：**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a>配置时区

若要在具有特定时区的 Linux 容器中运行 SQL Server, 请配置**TZ**环境变量。 若要查找正确的时区值, 请在 Linux bash 提示符下运行**tzselect**命令:

```bash
tzselect
```

选择时区后, **tzselect**将显示类似于以下内容的输出:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

你可以使用此信息在 Linux 容器中设置相同的环境变量。 下面的示例演示如何在`Americas/Los_Angeles`时区中的容器中运行 SQL Server:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>运行特定 SQL Server 容器映像

在某些情况下, 你可能不希望使用最新 SQL Server 容器映像。 若要运行特定 SQL Server 容器映像, 请使用以下步骤:

1. 确定要使用的版本的 Docker**标记**。 若要查看可用的标记, 请参阅[mssql-server-Linux Docker 中心页](https://hub.docker.com/_/microsoft-mssql-server)。

2. 用标记拉取 SQL Server 容器映像。 例如, 若要请求 RC1 映像, 请将`<image_tag>`以下命令中的替换`rc1`为。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要使用此映像运行新容器, 请在`docker run`命令中指定标记名称。 在下面的命令中, `<image_tag>`将替换为要运行的版本。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

还可以使用这些步骤来降级现有容器。 例如, 你可能想要回滚或降级正在运行的容器, 以便进行故障排除或测试。 若要降级正在运行的容器, 必须对数据文件夹使用持久性技术。 按照 "[升级" 一节](#upgrade)中所述的相同步骤进行操作, 但在运行新容器时指定较早版本的标记名称。

## <a id="version"></a>检查容器版本

如果想要了解正在运行的 docker 容器中的 SQL Server 版本, 请运行以下命令将其显示。 替换`<Container ID or name>`为目标容器 ID 或名称。 替换`<YourStrong!Passw0rd>`为 SA 登录名的 SQL Server 密码。

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

还可以确定目标 docker 容器映像的 SQL Server 版本和内部版本号。 以下命令显示**microsoft/mssql-Server-linux: 2017-最新**映像的 SQL Server 版本和生成信息。 它通过运行具有环境变量**PAL_PROGRAM_INFO = 1**的新容器来实现此功能。 生成的容器将立即退出, 并且`docker rm`该命令会将其删除。

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

前面的命令显示类似于以下输出的版本信息:

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a id="upgrade"></a>在容器中升级 SQL Server

若要将容器映像与 Docker 升级, 请首先确定升级版本的标记。 通过`docker pull`命令从注册表中提取此版本:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

这将更新任何新创建容器的 SQL Server 映像，但不会更新任何正在运行的容器中的 SQL Server。 为此，必须使用最新 SQL Server 容器映像创建新容器，并将数据迁移到该新容器。

1. 请确保对现有 SQL Server 容器使用[数据持久性技术](#persist)之一。 这样, 便可以启动具有相同数据的新容器。

1. 用`docker stop`命令停止 SQL Server 容器。

1. 使用`docker run`创建新的 SQL Server 容器, 并指定映射的主机目录或数据卷容器。 请确保对 SQL Server 升级使用特定标记。 新容器当前使用新版 SQL Server 和现有 SQL Server 数据。

   > [!IMPORTANT]
   > 目前仅支持 RC1、RC2 和 GA 之间的升级。

1. 在新容器中验证数据库和数据。

1. (可选) 删除旧容器`docker rm`。

## <a id="troubleshooting"></a> 故障排除

以下各节提供关于在容器中运行 SQL Server 的故障排除建议。

### <a name="docker-command-errors"></a>Docker 命令错误

如果任何`docker`命令都出现错误, 请确保 docker 服务正在运行, 并尝试以提升的权限运行。

例如, 在 Linux 上运行`docker`命令时, 可能会收到以下错误:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果在 Linux 上收到此错误, 请尝试运行以`sudo`开头的相同命令。 如果失败，验证 Docker 服务是否正在运行；如果没有，请启动它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 上, 验证是以管理员身份启动 PowerShell 还是命令提示符。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器启动错误

如果 SQL Server 容器无法运行，请尝试下列测试：

- 如果收到错误, 如 **"无法在网桥上创建端点 CONTAINER_NAME。启动代理时出错: 侦听 tcp 0.0.0.0: 1433 绑定: 地址已在使用中。 '** , 则尝试将容器端口1433映射到已在使用的端口。 在主机上本地运行 SQL Server 时可能发生此错误。 如果启动了两个 SQL Server 容器，并尝试将它们映射到同一主机端口，也可能发生此错误。 如果发生这种情况, `-p`请使用参数将容器端口1433映射到其他主机端口。 例如： 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- 如果收到错误 **, 如 "在 unix:///var/run/docker.sock 尝试连接到 Docker 后台程序套接字时获得权限拒绝":获取 http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: 拨号 unix/var/run/docker.sock: connect: 权限被拒绝** "尝试启动容器, 然后将用户添加到 Ubuntu 中的 docker 组。 然后注销并再次登录, 因为此更改会影响新会话。 

   ```bash
    usermod -aG docker $USER
    ```
- 检查是否有任何来自容器的错误消息。

    ```bash
    docker logs e69e056c702d
    ```

- 确保满足快速入门一文的 "[先决条件](quickstart-install-connect-docker.md#requirements)" 部分中指定的最小内存和磁盘要求。

- 如果正在使用任何容器管理软件，请确保它支持以根身份运行的容器进程。 容器中的 sqlservr 进程以根身份运行。

- 查看[SQL Server 安装和错误日志](#errorlogs)。

### <a name="enable-dump-captures"></a>启用转储捕获

如果 SQL Server 进程在容器内失败, 则应创建一个启用了**SYS_PTRACE**的新容器。 这会添加 Linux 功能以跟踪进程, 这是在发生异常时创建转储文件所必需的。 支持可以使用转储文件来帮助解决问题。 下面的 docker run 命令启用此功能。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 连接故障

如果无法连接到在容器中运行的 SQL Server 实例，请尝试下列测试：

- 查看`docker ps -a`输出的 "**状态**" 列, 确保 SQL Server 容器正在运行。 如果没有, 请`docker start <Container ID>`使用启动它。

- 如果映射到非默认主机端口（非 1433），请确保在连接字符串中指定端口。 可以在`docker ps -a`输出的 "**端口**" 列中查看端口映射。 例如，下列命令将 sqlcmd 连接至在端口 1401 上侦听的容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果与现有`docker run`的映射数据卷或数据卷容器一起使用, SQL Server 将忽略的`MSSQL_SA_PASSWORD`值。 改为使用来自 SQL Server 数据（在数据卷或数据卷容器中）的预配置 SA 用户密码。 验证所使用的 SA 密码是否与附加到的数据相关联。

- 查看[SQL Server 安装和错误日志](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性组

如果正在使用 Docker 和 SQL Server 可用性组，还有两个额外要求。

- 映射用于副本通信的端口（默认为 5022）。 例如, 将`docker run`指定`-p 5022:5022`为命令的一部分。

- 用`-h YOURHOSTNAME` `docker run`命令的参数显式设置容器主机名。 配置可用性组时使用该主机名。 如果不指定`-h`, 则默认为容器 ID。

### <a id="errorlogs"></a>SQL Server 安装和错误日志

可以在 **/var/opt/mssql/log**中查看 SQL Server 设置和错误日志。 如果容器未运行，请首先启动它。 然后使用交互式命令提示符来检查日志。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

从容器内的 bash 会话运行下列命令：

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果在创建容器时将主机目录装载到 **/var/opt/mssql** , 则可以在**日志**子目录中查看主机上映射的路径。

## <a name="next-steps"></a>后续步骤

通过[快速入门](quickstart-install-connect-docker.md), 开始使用 Docker 上的 SQL Server 2017 容器映像。

另请参阅[mssql-Docker GitHub 存储库](https://github.com/Microsoft/mssql-docker), 了解资源、反馈和已知问题。

[探索 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
