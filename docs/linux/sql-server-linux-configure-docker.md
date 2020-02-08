---
title: Docker 上的 SQL Server 的配置选项
description: 探索在 Docker 中使用 SQL Server 2017 和 2019 容器映像并与其交互的不同方法。 这包括保留数据、复制文件和故障排除。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76162628"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上配置 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何通过 Docker 配置和使用 [mssql-server-linux 容器映像](https://hub.docker.com/_/microsoft-mssql-server)。 

有关其他部署方案，请参阅：

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - 大数据群集](../big-data-cluster/deploy-get-started.md)

此映像包含在 Linux 上运行的 SQL Server（基于 Ubuntu 16.04）。 它可与 Linux 上或用于 Mac/Windows 的 Docker 上的 Docker 引擎 1.8+ 配合使用。

> [!NOTE]
> 本文专门重点介绍 mssql-server-linux 映像的使用。 虽然没有介绍 Windows 映像，但可在 [mssql-server-windows Docker Hub 页](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)上找到关于它的详细信息。

> [!IMPORTANT]
> 在选择运行 SQL Server 容器以用于生产用例之前，请查看 [SQL Server 容器的支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)，以确保在支持的配置上运行。

本视频时长 6 分钟，介绍了如何在容器上运行 SQL Server：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>拉取并运行容器映像

若要拉取并运行 SQL Server 2017 和 SQL Server 2019 的 Docker 容器映像，请按照以下快速入门中的先决条件和步骤执行操作：

- [使用 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md?view=sql-server-2017)
- [使用 Docker 运行 SQL Server 2019 容器映像](quickstart-install-connect-docker.md?view=sql-server-ver15)

本配置文章在以下部分中提供其他使用方案。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> 运行基于 RHEL 的容器映像

SQL Server Linux 容器映像的文档指向基于 Ubuntu 的容器。 从 SQL Server 2019 开始，可使用基于 Red Hat Enterprise Linux (RHEL) 的容器。 在所有 docker 命令中，将容器存储库从 mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04 更改为 mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8   。

例如，以下命令拉取使用 RHEL 8 的 SQL Server 2019 容器的累积更新 1：

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> 运行生产容器映像

上一部分中的快速入门从 Docker Hub 运行 SQL Server 的免费 Developer Edition。 如果想要运行生产容器映像（例如 Enterprise、Standard 或 Web Edition），大部分信息仍然适用。 但是，存在一些差异，此处将其列出。

- 如果拥有有效的许可证，则只能在生产环境中使用 SQL Server。 可在[此处](https://go.microsoft.com/fwlink/?linkid=857693)获取免费的 SQL Server Express 生产许可证。 SQL Server Standard 和 Enterprise Edition 许可证可通过 [Microsoft 批量许可](https://www.microsoft.com/licensing/default.aspx)获得。


- Developer 容器映像也可以配置为运行生产版本。 使用以下步骤运行生产版本：

查看[快速入门](quickstart-install-connect-docker.md)中的要求并运行过程。 必须使用 **MSSQL_PID** 环境变量指定生产版本。 以下示例介绍如何运行 Enterprise Edition 的最新 SQL Server 2017 容器映像：

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> 通过将值 **Y** 传递给环境变量 **ACCEPT_EULA** 并将版本值传递给 **MSSQL_PID**，你表明自己拥有打算使用的 SQL Server 版本的现行有效有许可证。 你还同意自己对在 Docker 容器映像中运行的 SQL Server 软件的使用将受 SQL Server 许可条款的约束。

> [!NOTE]
> 有关 **MSSQL_PID** 的可能值的完整列表，请参阅[在 Linux 上使用环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

::: moniker-end

## <a name="connect-and-query"></a>连接和查询

可从容器外部或内部对容器中的 SQL Server 进行连接和查询。 以下部分介绍这两种方案。 

### <a name="tools-outside-the-container"></a>容器外的工具

可从支持 SQL 连接的任何 Linux、Windows 或 macOS 外部工具连接到 Docker 计算机上的 SQL Server 实例。 一些常用工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [适用于 Windows 的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

以下示例使用 **sqlcmd** 连接到在 Docker 容器中运行的 SQL Server。 连接字符串中的 IP 地址为运行容器的主机的 IP 地址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果映射的主机端口不是默认的 **1433**，请将该端口添加到连接字符串中。 例如，如果在 `docker run` 命令中指定了 `-p 1400:1433`，则请通过显式指定端口 1400 来进行连接。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器内的工具

从 SQL Server 2017 开始，容器映像中加入了 [SQL Server 命令行工具](sql-server-linux-setup-tools.md)。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

1. 使用 `docker exec -it` 命令在运行的容器内部启动交互式 Bash Shell。 在以下示例中，`e69e056c702d` 是容器 ID。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 并非始终需要指定完整的容器 ID。只需指定能够唯一标识它的足够字符即可。 因此，在本示例中，使用 `e6` 或 `e69` 足矣，无需使用完整 ID。

2. 在容器内部使用 sqlcmd 进行本地连接。 请注意，默认情况下，sqlcmd 不在路径之中，因此需要指定完整的路径。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 使用 sqlcmd 完成操作后，键入 `exit`。

4. 使用交互式命令提示符完成操作后，键入 `exit`。 退出交互式 Bash Shell 后，容器将继续运行。

## <a name="run-multiple-sql-server-containers"></a>运行多个 SQL Server 容器

Docker 支持在同一主机上运行多个 SQL Server 容器。 对要求在同一主机上运行多个 SQL Server 实例的方案使用此解决办法。 每个容器必须在不同的端口上公开自己。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

以下示例创建两个 SQL Server 2017 容器，并将它们映射到主机的 **1401** 和 **1402**端口。

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

以下示例创建两个 SQL Server 2019 容器，并将它们映射到主机的 1401 和 1402 端口   。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

现在，两个 SQL Server 实例在单独的容器内运行。 客户端可通过使用 Docker 主机的 IP 地址和容器的端口号连接到每个 SQL Server 实例。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> 创建自定义容器

可以创建自己的 [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) 来创建自定义 SQL Server 容器。 有关详细信息，请参阅[组合使用 SQL Server 和节点应用程序的演示](https://github.com/twright-msft/mssql-node-docker-demo-app)。 如果创建了自己的 Dockerfile，请注意前台进程，因为此进程控制容器的生命周期。 如果它退出，容器将关闭。 例如，如果想要运行脚本并启动 SQL Server，请确保 SQL Server 进程是最右侧的命令。 所有其他命令都会在后台运行。 以下命令在 Dockerfile 中对此进行说明：

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果撤销上一个示例中的命令，则容器将在 do-my-sql-commands.sh 脚本完成时关闭。

## <a id="persist"></a> 保留数据

即使通过 `docker stop` 和 `docker start` 重启容器，SQL Server 配置仍会更改，且数据库文件依然保留在容器中。 但是，如果使用 `docker rm` 删除容器，则会删除容器中的所有内容，包括 SQL Server 和数据库。 以下部分介绍如何使用**数据卷**保留数据库文件（即使关联的容器已被删除）。

> [!IMPORTANT]
> 对于 SQL Server，了解 Docker 中的数据持久性至关重要。 除本部分讨论的内容外，请参阅有关[如何在 Docker 容器中管理数据](https://docs.docker.com/engine/tutorials/dockervolumes/)的 Docker 文档。

### <a name="mount-a-host-directory-as-data-volume"></a>将主机目录作为数据卷装载

第一种方法是在主机上将目录作为容器中的数据卷装载。 为此，请将 `docker run` 命令与 `-v <host directory>:/var/opt/mssql` 标志配合使用。 这允许在容器执行之间还原数据。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

借助此方法，还能共享和查看 Docker 外部的主机上的文件。

> [!IMPORTANT]
> Windows 上的 Docker 的主机卷映射当前不支持映射完整的 `/var/opt/mssql` 目录  。 但是，你可以将子目录（如 `/var/opt/mssql/data`）映射到主机。

> [!IMPORTANT]
> 目前不支持 Mac 上的 Docker 与 Linux 映像上的 SQL Server 之间的主机卷映射  。 请改为使用数据卷容器。 此限制特定于 `/var/opt/mssql` 目录。 从已装载目录进行读取操作可正常运行。 例如，可在 Mac 上使用 –v 装载主机目录，并通过驻留在主机上的 .bak 文件还原备份。

### <a name="use-data-volume-containers"></a>使用数据卷容器

第二种方法是使用数据卷容器。 可通过指定卷名（而不是包含 `-v` 参数的主机目录）来创建数据卷容器。 以下示例创建名为 **sqlvolume** 的共享数据卷。

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> 早期版本的 Docker 不支持通过此方法在 run 命令中隐式创建数据卷。 在这种情况下，请使用 Docker 文档[创建和装载数据卷容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)中列出的显式步骤。

即使停止并删除此容器，数据卷仍然存在。 可使用 `docker volume ls` 命令进行查看。

```bash
docker volume ls
```

如果随后创建另一个具有相同卷名的容器，则新容器会使用卷中包含的相同 SQL Server 数据。

若要删除数据卷容器，请使用 `docker volume rm` 命令。

> [!WARNING]
> 如果删除数据卷容器，则该容器中的所有 SQL Server 数据都会被*永久*删除。

### <a name="backup-and-restore"></a>备份和还原

除这些容器技术外，还可使用 SQL Server 标准备份和还原技术。 可通过备份文件来保护数据，或将数据移至其他 SQL Server 实例。 有关详细信息，请参阅[在 Linux 上备份和还原 SQL Server 数据库](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如果要创建备份，请确保在容器外部创建或复制备份文件。 否则，一旦删除容器，备份文件也将随之删除。

## <a name="execute-commands-in-a-container"></a>在容器中执行命令

如果正在运行容器，则可从主机终端在容器内部执行命令。

若要获取容器 ID，请运行：

```bash
docker ps
```

若要在容器中启动 Bash 终端，请运行：

```bash
docker exec -it <Container ID> /bin/bash
```

现在，可以像在容器内的终端上那样运行这些命令。 完成后，键入 `exit`。 这将退出交互式命令会话，但容器会继续运行。

## <a name="copy-files-from-a-container"></a>从容器复制文件

若要从容器复制文件，请使用以下命令：

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

若要将文件复制到容器中，请使用以下命令：

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
## <a id="tz"></a> 配置时区

若要在具有特定时区的 Linux 容器中运行 SQL Server，请配置 `TZ` 环境变量。 若要查找正确的时区值，请从 Linux bash 提示符运行 `tzselect` 命令：

```bash
tzselect
```

选择时区后，`tzselect` 显示类似以下内容的输出：

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

可使用此信息在 Linux 容器中设置相同的环境变量。 以下示例介绍如何在 `Americas/Los_Angeles` 时区的容器中运行 SQL Server：

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
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a id="tags"></a> 运行特定 SQL Server 容器映像

在某些情况下，可能不希望使用最新的 SQL Server 容器映像。 若要运行特定 SQL Server 容器映像，请使用以下步骤：

1. 确定想要使用的版本的 Docker **标记**。 若要查看可用标记，请参阅 [mssql-server-linux Docker Hub 页](https://hub.docker.com/_/microsoft-mssql-server)。

2. 使用标记拉取 SQL Server 容器映像。 例如，若要拉取 RC1 映像，请将以下命令中的 `<image_tag>` 替换为 `rc1`。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要使用该映像运行新容器，请在 `docker run` 命令中指定标记名称。 在以下命令中，将 `<image_tag>` 替换为想要运行的版本。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

这些步骤也可用于降级现有容器。 例如，你可能会希望回滚或降级正在运行的容器以进行故障排除或测试。 若要降级正在运行的容器，必须对数据文件夹使用持久性技术。 按照[升级部分](#upgrade)所述的相同步骤进行操作，但在运行新容器时指定早期版本的标记名称。

## <a id="version"></a> 检查容器版本

如果想要了解正在运行的 docker 容器中的 SQL Server 的版本，请运行以下命令以显示它。 将 `<Container ID or name>` 替换为目标容器 ID 或名称。 将 `<YourStrong!Passw0rd>` 替换为 SA 登录名的 SQL Server 密码。

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

还可以标识目标 docker 容器映像的 SQL Server 版本和生成号。 以下命令显示 mcr.microsoft.com/mssql/server:2017-latest 映像的 SQL Server 版本和生成信息  。 它通过运行具有环境变量 **PAL_PROGRAM_INFO=1** 的新容器来实现此目的。 生成的容器会立即退出，且 `docker rm` 命令会将其删除。

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

上一个命令显示类似以下输出的版本信息：

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

## <a id="upgrade"></a> 升级容器中的 SQL Server

若要使用 Docker 升级容器映像，请先确定升级版本的标记。 使用 `docker pull` 命令从注册表中拉取此版本：

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

此操作会更新创建的任何新容器的 SQL Server 映像，但不会更新任何正在运行的容器中的 SQL Server。 为此，必须使用最新的 SQL Server 容器映像创建新容器，并将数据迁移到该新容器。

1. 确保为现有 SQL Server 容器使用一种[数据持久性技术](#persist)。 这样便可以启动具有相同数据的新容器。

1. 使用 `docker stop` 命令停止 SQL Server 容器。

1. 使用 `docker run` 创建新的 SQL Server 容器，并指定映射主机目录或数据卷容器。 确保使用特定标记进行 SQL Server 升级。 新容器现在使用新版 SQL Server 和现有 SQL Server 数据。

   > [!IMPORTANT]
   > 目前仅支持在 RC1、RC2 和 GA 之间升级。

1. 在新容器中验证数据库和数据。

1. 使用 `docker rm` 删除旧容器（可选）。

## <a id="buildnonrootcontainer"></a> 生成并运行非根 SQL Server 2017 容器

按照以下步骤生成以 `mssql`（非根）用户身份启动的 SQL Server 2017 容器。

> [!NOTE]
> SQL Server 2019 容器自动以非根身份启动，因此以下步骤仅适用于 SQL Server 2017 容器，默认情况下，该容器以根身份启动。

1. 下载[适用于非根 SQL Server 容器的示例dockerfile](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile)，并将其另存为 `dockerfile`。

2. 在 dockerfile 目录的上下文中运行以下命令，生成非根 SQL Server 容器：

```bash
cd <path to dockerfile>
docker build -t 2017-latest-non-root .
```

3. 启动容器。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
```

> [!NOTE]
> 非根 SQL Server 容器需要 `--cap-add SYS_PTRACE` 标志来生成用于排除故障的转储。

4. 检查是否以非根用户的身份运行容器：

docker 执行到容器中。
```bash
docker exec -it sql1 bash
```

运行 `whoami`，这将返回容器中运行的用户。

```bash
whoami
```

## <a id="nonrootuser"></a>在主机上以其他非根用户的身份运行容器

若要以其他非根用户的身份运行 SQL Server 容器，请将 -u 标志添加到 docker run 命令。 非根容器具有以下限制：必须作为根组的一部分运行，除非已将卷装载到非根用户可以访问的“/var/opt/mssql”。 根组不向非根用户授予任何额外的根权限。

**以具有 UID 4000 的用户身份运行**

可使用自定义 UID 启动 SQL Server。 例如，以下命令使用 UID 4000 启动 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> 确保 SQL Server 容器具有命名用户，如“mssql”或“root”，否则 SQLCMD 将无法在容器中运行。 可通过在容器中运行 `whoami` 来检查是否以命名用户的身份运行 SQL Server 容器。

**以根用户的身份运行非根容器**

如果需要，以根用户的身份运行非根容器。 这还会将所有文件权限自动授予容器，因为容器具有更高的特权。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**在主机计算机上以用户的身份运行**

可使用以下命令在主机计算机上以现有用户身份启动 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**以其他用户和组的身份运行**

可使用自定义用户和组启动 SQL Server。 在此示例中，已装载的卷具有为主机计算机上的用户或组配置的权限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="storagepermissions"></a>为非根容器配置持久存储权限

若要允许非根用户访问已装载的卷上的 DB 文件，请确保运行容器所用的用户/组可以接触持久文件存储。  

可通过此命令获取数据库文件的当前所有权。

```bash
ls -ll <database file dir>
```

如果 SQL Server 无权访问持久数据库文件，请运行以下命令之一。

**授予对 DB 文件的根组读/写访问权限**

授予对以下目录的根组权限，使非根 SQL Server 容器有权访问数据库文件。

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**将非根用户设置为文件的所有者。**

这可以是默认的非根用户，也可以是要指定的任何其他非根用户。 在此示例中，我们将 UID 10001 设置为非根用户。

```bash
chown -R 10001:0 <database file dir>
```

## <a id="changefilelocation"></a>更改默认文件位置

添加 `MSSQL_DATA_DIR` 变量以在 `docker run` 命令中更改数据目录，然后将卷装载到容器的用户有权访问的位置。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="troubleshooting"></a> 故障排除

以下部分提供关于在容器中运行 SQL Server 的故障排除建议。

### <a name="docker-command-errors"></a>Docker 命令错误

如果遇到任何 `docker` 命令错误，请确保 Docker 服务正在运行，并尝试通过提升的权限运行。

例如，在 Linux 上运行 `docker` 命令时可能会遇到以下错误：

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果在 Linux 上遇到此错误，请尝试对相同的命令加上 `sudo` 前缀，然后再运行。 如果失败，请验证 Docker 服务是否正在运行；如果没有，请启动它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 上，验证并确保以管理员身份启动 PowerShell 或命令提示符。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器启动错误

如果 SQL Server 容器无法运行，请尝试以下测试：

- 如果遇到 **“无法在网桥上创建终结点 CONTAINER_NAME。启动代理时出错: 侦听 tcp 0.0.0.0:1433 绑定: 地址已被使用。”** 等错误，这表示你正尝试将容器端口 1433 映射到某个正在使用的端口。 在主机上本地运行 SQL Server 时可能发生此错误。 如果启动两个 SQL Server 容器，并尝试将它们映射到同一主机端口，也可能发生此错误。 如果发生此错误，请使用 `-p` 参数将容器端口 1433 映射到不同的主机端口。 例如： 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- 如果在尝试启动容器时遇到 **“在 unix:///var/run/docker.sock 尝试连接到 Docker 守护程序套接字时获取权限被拒绝:获取 http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: 权限被拒绝”** 等错误，请将用户添加到 Ubuntu 中的 docker 组。 然后注销并重新登录，因为此更改将影响新会话。 

   ```bash
    usermod -aG docker $USER
   ```
- 检查是否有任何来自容器的错误消息。

    ```bash
    docker logs e69e056c702d
    ```

- 确保符合快速入门文章的[先决条件](quickstart-install-connect-docker.md#requirements)部分中指定的最低内存和磁盘要求。

- 如果使用任何容器管理软件，请确保它支持以根身份运行的容器进程。 容器中的 sqlservr 进程以根身份运行。

- 查看 [SQL Server 安装和错误日志](#errorlogs)。

### <a name="enable-dump-captures"></a>启用转储捕获

如果 SQL Server 进程在容器内失败，则应创建一个启用了 **SYS_PTRACE** 的新容器。 此操作可添加用于跟踪进程的 Linux 功能，该功能是在出现异常时创建转储文件所必需的。 支持人员可以使用转储文件来帮助对问题进行故障排除。 以下 docker run 命令可启用此功能。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 连接故障

如果无法连接到在容器中运行的 SQL Server 实例，请尝试以下测试：

- 通过查看 `docker ps -a` 输出的“状态”列，确保 SQL Server 容器正在运行  。 如果未在运行，则使用 `docker start <Container ID>` 启动它。

- 如果映射到非默认主机端口（非 1433），请确保在连接字符串中指定端口。 可在 `docker ps -a` 输出的“端口”列中查看端口映射  。 例如，以下命令将 sqlcmd 连接至正在侦听端口 1401 的容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果将 `docker run` 和现有的映射数据卷或数据卷容器配合使用，SQL Server 会忽略 `MSSQL_SA_PASSWORD` 的值。 改为使用来自 SQL Server 数据（数据卷或数据卷容器中）的预配置 SA 用户密码。 验证所使用的 SA 密码是否与附加到的数据相关联。

- 查看 [SQL Server 安装和错误日志](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性组

如果将 Docker 与 SQL Server 可用性组配合使用，则还有两个附加要求。

- 映射用于副本通信的端口（默认为 5022）。 例如，将 `-p 5022:5022` 指定为 `docker run` 命令的一部分。

- 使用 `docker run` 命令的 `-h YOURHOSTNAME` 参数显式设置容器主机名。 配置可用性组时会使用此主机名。 如果不使用 `-h` 来指定它，它会默认使用容器 ID。

### <a id="errorlogs"></a> SQL Server 安装和错误日志

可在 **/var/opt/mssql/log** 中查看 SQL Server 安装和错误日志。 如果容器未在运行，请先启动它。 然后使用交互式命令提示符来检查日志。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

从容器内的 bash 会话运行以下命令：

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果在创建容器时将主机目录装载到了 **/var/opt/mssql**，可改为在主机上映射路径的 **log** 子目录中进行查找。

## <a name="next-steps"></a>后续步骤

通过查看[快速入门](quickstart-install-connect-docker.md)，开始在 Docker 上使用 SQL Server 2017 容器映像。

另请查看 [mssql-docker GitHub 存储库](https://github.com/Microsoft/mssql-docker)，获取资源、反馈和已知问题。

[探索 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
