---
title: Docker 上的 SQL Server 配置选项 |Microsoft Docs
description: 了解不同使用和与 SQL Server 2017 和 2019年预览版容器映像在 Docker 中的进行交互的方式。 这包括保存数据，将文件，复制和故障排除。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: ae57a6f453cf15dbb22158b49aad990cc0c3df67
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100732"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上配置 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章介绍了如何配置和使用[mssql server linux 容器映像](https://hub.docker.com/r/microsoft/mssql-server-linux/)使用 Docker。 此映像包含在 Linux（基于 Ubuntu 16.04）上运行的 SQL Server。 它可与适用于 Linux 的 Docker 引擎 1.8 以上版本或适用于 Mac/Windows 的 Docker 配合使用。

> [!NOTE]
> 本文专门重点介绍使用 mssql server linux 映像。 未介绍 Windows 映像，但您可以了解有关它的[mssql server windows Docker 中心页](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

若要请求和运行 SQL Server 2017 和 SQL Server 2019 预览的容器映像的 Docker，请执行的先决条件和以下快速入门中的步骤：

- [使用 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md?view=sql-server-2017)
- [使用 Docker 运行 SQL Server 2019 预览版容器映像](quickstart-install-connect-docker.md?view=sql-server-ver15)

配置本文提供了以下各节中的其他使用方案。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> 运行基于 RHEL 的容器映像

SQL Server Linux 容器映像上的文档的所有点基于 Ubuntu 的容器。 从 SQL Server 2019 预览开始，可以使用基于 Red Hat Enterprise Linux (RHEL) 上的容器。 更改从容器存储库**mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu**到**mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0**中的所有 docker 命令。

例如，以下命令拉取使用 RHEL 的最新 SQL Server 2019 预览版容器：

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.2
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.2
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> 运行生产容器映像

在快速入门中上一节从 Docker 中心运行 SQL Server 免费的 Developer 的 edition。 如果你想要运行生产容器映像，如 Enterprise、 Standard edition 或 Web edition，大部分信息仍然适用。 但是，有此处所述的一些差异。

- 仅可以使用 SQL Server 生产环境中如果有有效的许可证。 你可以获取免费的 SQL Server Express 生产许可证[此处](https://go.microsoft.com/fwlink/?linkid=857693)。 SQL Server Standard edition 和 Enterprise Edition 许可证是可通过[Microsoft 批量许可](https://www.microsoft.com/licensing/default.aspx)。


- 开发人员的容器映像可以配置为运行生产版。 使用以下步骤来运行生产版：

查看要求，并运行过程[快速入门](quickstart-install-connect-docker.md)。 必须指定你使用的生产版**MSSQL_PID**环境变量。 下面的示例演示如何为 Enterprise Edition 运行最新的 SQL Server 2017 容器映像：

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
      > By passing the value **Y** to the environment variable **ACCEPT_EULA** and an edition value to **MSSQL_PID**, you are expressing that you have a valid and existing license for the edition and version of SQL Server that you intend to use. You also agree that your use of SQL Server software running in a Docker container image will be governed by the terms of your SQL Server license.

      > [!NOTE]
      > For a full list of possible values for **MSSQL_PID**, see [Configure SQL Server settings with environment variables on Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>连接和查询

可以从容器外部或内部对容器中的 SQL Server 进行连接和查询。 以下各节介绍了这两种方案。 

### <a name="tools-outside-the-container"></a>容器外的工具

可以从支持 SQL 连接的任何 Linux、Windows 或 macOS 外部工具连接到 Docker 计算机上的 SQL Server 实例。 一些常用工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [适用于 Windows 的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

下面的示例使用**sqlcmd**连接到 Docker 容器中运行的 SQL Server。 连接字符串中的 IP 地址是运行容器的主机的 IP 地址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果映射不是默认的主机端口**1433年**，将该端口添加到连接字符串。 例如，如果您指定`-p 1400:1433`在您`docker run`命令，然后显式连接指定端口 1400年。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器内的工具

从 SQL Server 2017 预览版[SQL Server 命令行工具](sql-server-linux-setup-tools.md)包含在容器映像。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

1. 使用 `docker exec -it` 命令在运行的容器内部启动交互式 Bash Shell。 在下面的示例`e69e056c702d`是容器 id。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 无需始终指定完整的容器 ID。只需要指定足够的字符，能够唯一标识它即可。 因此在此示例中，它可能不足以使用`e6`或`e69`而不是完整 id。

2. 一旦位于容器内部，使用 sqlcmd 进行本地连接。 请注意， 默认情况下，sqlcmd 不在路径之中，因此需要指定完整的路径。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 使用 sqlcmd 完成操作后，键入`exit`。

4. 使用交互式命令提示符完成操作后，键入`exit`。 退出交互式 Bash Shell 后，容器将继续运行。

## <a name="run-multiple-sql-server-containers"></a>运行多个 SQL Server 容器

Docker 支持在同一主机上运行多个 SQL Server 容器。 这就为要求在同一主机上运行多个 SQL Server 实例的方案提供了解决办法。 每个容器必须在一个不同的端口上公开自身。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

下面的示例创建两个 SQL Server 2017 容器，并将它们映射到端口**1401年**并**1402年**主机计算机上。

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

下面的示例创建两个 SQL Server 2019 预览版容器，并将它们映射到端口**1401年**并**1402年**主机计算机上。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
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

## <a id="customcontainer"></a> 创建自定义的容器

可以创建您自己[Dockerfile](https://docs.docker.com/engine/reference/builder/#usage)创建自定义的 SQL Server 容器。 有关详细信息，请参阅[结合了 SQL Server 和 Node 应用程序的演示](https://github.com/twright-msft/mssql-node-docker-demo-app)。 如果您创建你自己的 Dockerfile，请注意前台进程，因为此过程控制容器的生命周期。 如果退出，容器会关闭。 例如，如果你想要运行脚本并启动 SQL Server，请确保 SQL Server 进程是最右边的命令。 在后台运行的所有其他命令。 Dockerfile 中的以下命令所示：

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果撤消上一示例中的命令，容器将执行操作-我的 sql-commands.sh 脚本完成后将关闭。

## <a id="persist"></a> 保存数据

即使您重新启动的容器的容器中保持 SQL Server 配置更改和数据库文件的`docker stop`和`docker start`。 但是，如果删除与容器`docker rm`，容器中将删除所有内容，包括 SQL Server 和数据库。 以下部分介绍如何使用**数据卷**持久保存在数据库文件，即使关联的容器已被删除。

> [!IMPORTANT]
> 就 SQL Server 而言，了解 Docker 中的数据持久性至关重要。 除了在本部分中讨论，请参阅 Docker 文档[如何管理 Docker 容器中的数据](https://docs.docker.com/engine/tutorials/dockervolumes/)。

### <a name="mount-a-host-directory-as-data-volume"></a>将主机目录装载为数据卷

第一种方法是在主机上装载目录，将其作为容器中的数据卷。 若要执行此操作，请使用`docker run`命令与`-v <host directory>:/var/opt/mssql`标志。 这允许在容器执行之间还原数据。

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

::: moniker-end

通过此方法，还能共享和查看位于主机上、Docker 外的文件。

> [!IMPORTANT]
> 当前不支持 Mac 上的 Docker 与 Linux 映像上 SQL Server 的主机卷映射。 请改为使用数据卷容器。 此限制是特定于`/var/opt/mssql`目录。 从已装载目录进行读取操作可正常运行。 例如，可以装载在 Mac 上使用-v 主机目录，并驻留在主机的.bak 文件从还原备份。

### <a name="use-data-volume-containers"></a>使用数据卷容器

第二个方法是使用数据卷容器。 可以通过指定卷名称而不是与一个主机目录中创建数据卷容器`-v`参数。 下面的示例创建名为的共享的数据卷**sqlvolume**。

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```
::: moniker-end

> [!NOTE]
> 早期版本的 Docker 不支持通过此方法在 run 命令中隐式创建数据卷。 在这种情况下，使用 Docker 文档中所述的显式步骤[创建和装载数据卷容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)。

即使停止并删除此容器，数据卷仍然存在。 您可以查看它与`docker volume ls`命令。

```bash
docker volume ls
```

如果稍后又创建了另一个具有相同卷名的容器，则这个新容器将使用卷中包含的相同 SQL Server 数据。

若要删除数据卷容器，请使用`docker volume rm`命令。

> [!WARNING]
> 如果您删除数据卷容器，容器中的任何 SQL Server 数据是*永久*删除。

### <a name="backup-and-restore"></a>备份和还原

除这些容器技术外，还可使用 SQL Server 标准备份和还原技术。 可通过备份文件来保护数据，或将数据移动至其他 SQL Server 实例。 有关详细信息，请参阅[SQL Server 备份和还原 Linux 上的数据库](sql-server-linux-backup-and-restore-database.md)。

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
docker exec -ti <Container ID> /bin/bash
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

## <a name="copy-files-into-a-container"></a>将文件复制到容器

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

## <a id="tags"></a> 运行特定的 SQL Server 容器映像

提供了的方案，您可能不想要使用最新的 SQL Server 容器映像。 若要运行特定的 SQL Server 容器映像，请使用以下步骤：

1. 标识 Docker**标记**对于你想要使用的版本。 若要查看可用的标记，请参阅[mssql server linux Docker 中心页](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

2. 提取 SQL Server 容器映像的标记。 例如，若要提取 RC1 映像，替换`<image_tag>`在以下命令中使用`rc1`。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要使用该映像运行新容器，指定标记名称中的`docker run`命令。 在以下命令，将为`<image_tag>`与你想要运行的版本。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

此外可以使用这些步骤降级现有容器。 例如，您可能要回滚或降级进行故障排除或测试正在运行的容器。 若要降级正在运行的容器，你必须使用暂留技术数据文件夹。 按照相同的步骤中所述[升级部分](#upgrade)，但在运行新容器时指定的较旧版本的标记名称。

## <a id="version"></a> 检查容器版本

如果你想要知道正在运行的 docker 容器中的 SQL Server 的版本，运行以下命令以显示它。 替换为`<Container ID or name>`具有目标容器 ID 或名称。 替换为`<YourStrong!Passw0rd>`替换为 SA 登录名的 SQL Server 密码。

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

此外可以确定 SQL Server 版本和内部版本号为目标的 docker 容器映像。 下面的命令显示的 SQL Server 版本和内部版本信息**microsoft/mssql-server-linux:2017-最新**映像。 这是通过使用环境变量运行新的容器**PAL_PROGRAM_INFO = 1**。 生成的容器可立即退出，和`docker rm`命令将其删除。

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

前面的命令显示版本信息类似于以下输出：

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

## <a id="upgrade"></a> 在容器中的 SQL Server 升级

若要升级使用 Docker 容器映像，首先确定为升级版本的标记。 从注册表中拉取此版本`docker pull`命令：

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

这将更新任何新创建容器的 SQL Server 映像，但不会更新任何正在运行的容器中的 SQL Server。 为此，必须使用最新 SQL Server 容器映像创建新容器，并将数据迁移到该新容器。

1. 请确保你使用的之一[数据持久性技术](#persist)为现有 SQL Server 容器。 这使您可以使用相同的数据启动新的容器。

1. 停止 SQL Server 容器与`docker stop`命令。

1. 创建新的 SQL Server 容器与`docker run`并指定一个映射的主机目录或数据卷容器。 请确保 SQL Server 升级为使用特定的标记。 新容器当前使用新版 SQL Server 和现有 SQL Server 数据。

   > [!IMPORTANT]
   > 仅支持 RC1 和 RC2，GA 之间在此时间进行升级。

1. 在新容器中验证数据库和数据。

1. （可选） 删除与旧容器`docker rm`。

## <a id="troubleshooting"></a> 故障排除

以下各节提供关于在容器中运行 SQL Server 的故障排除建议。

### <a name="docker-command-errors"></a>Docker 命令错误

如果出现任何错误`docker`命令，请确保 docker 服务正在运行，并尝试使用提升的权限运行。

例如，在 Linux 上，你可能会收到以下错误时运行`docker`命令：

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果在 Linux 上收到此错误，请尝试运行相同命令加`sudo`。 如果失败，验证 Docker 服务是否正在运行；如果没有，请启动它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 中，验证将启动 PowerShell 或以管理员身份在命令提示符。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器启动错误

如果 SQL Server 容器无法运行，请尝试下列测试：

- 如果你收到错误，例如**无法在网桥上创建终结点 CONTAINER_NAME。启动代理时出错： 侦听 tcp 0.0.0.0:1433 绑定： 地址已在使用。**，然后尝试将容器端口 1433年映射到已在使用的端口。 在主机上本地运行 SQL Server 时可能发生此错误。 如果启动了两个 SQL Server 容器，并尝试将它们映射到同一主机端口，也可能发生此错误。 如果发生这种情况，使用`-p`参数将容器端口 1433年映射到不同的主机端口。 例如： 

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
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu`.
    ```

::: moniker-end

- 检查是否有任何来自容器的错误消息。

    ```bash
    docker logs e69e056c702d
    ```

- 请确保满足中指定的最小内存和磁盘要求[要求](#requirements)本文的部分。

- 如果正在使用任何容器管理软件，请确保它支持以根身份运行的容器进程。 容器中的 sqlservr 进程以根身份运行。

- 审阅[SQL Server 安装程序和错误日志](#errorlogs)。

### <a name="enable-dump-captures"></a>启用转储捕获

如果 SQL Server 进程在容器内失败，则应创建具有的新容器**SYS_PTRACE**启用。 这会添加跟踪过程中，这是用于创建在出现异常的转储文件所必需的 Linux 功能。 支持可以使用转储文件以帮助排查问题。 以下 docker run 命令启用此功能。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 连接故障

如果无法连接到在容器中运行的 SQL Server 实例，请尝试下列测试：

- 请确保 SQL Server 容器正在运行通过查看**状态**列`docker ps -a`输出。 如果没有，请使用`docker start <Container ID>`来启动它。

- 如果映射到非默认主机端口（非 1433），请确保在连接字符串中指定端口。 可以查看在端口映射**端口**列`docker ps -a`输出。 例如，下列命令将 sqlcmd 连接至在端口 1401 上侦听的容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果您使用了`docker run`现有的映射的数据卷或数据卷容器，使用 SQL Server 会忽略的值`MSSQL_SA_PASSWORD`。 改为使用来自 SQL Server 数据（在数据卷或数据卷容器中）的预配置 SA 用户密码。 验证所使用的 SA 密码是否与附加到的数据相关联。

- 审阅[SQL Server 安装程序和错误日志](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性组

如果正在使用 Docker 和 SQL Server 可用性组，还有两个额外要求。

- 映射用于副本通信的端口（默认为 5022）。 例如，指定`-p 5022:5022`作为的一部分在`docker run`命令。

- 显式设置在容器主机名`-h YOURHOSTNAME`参数的`docker run`命令。 配置可用性组时使用该主机名。 如果未指定其与`-h`，它将默认为容器 id。

### <a id="errorlogs"></a> SQL Server 安装程序和错误日志

您可以查看 SQL Server 安装程序和错误日志 **/var/opt/mssql/log**。 如果容器未运行，请首先启动它。 然后使用交互式命令提示符来检查日志。

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
> 如果装载到主机目录 **/var/opt/mssql**创建容器时，您可以改为查看**日志**映射的路径在主机上的子目录。

## <a name="next-steps"></a>后续步骤

开始使用 Docker 上的 SQL Server 2017 容器映像通过[快速入门](quickstart-install-connect-docker.md)。

此外，请参阅[mssql-docker GitHub 存储库](https://github.com/Microsoft/mssql-docker)了解资源、 反馈和已知的问题。

[浏览 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
