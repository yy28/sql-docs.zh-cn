---
title: 保护 SQL Server Docker 容器
description: 了解保护 SQL Server Docker 容器的不同方法，以及如何在主机上以不同的非根用户身份运行容器
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 10d2eb061a4ee6d9ff9c8d0594561667dd882dc9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511558"
---
# <a name="secure-sql-server-docker-containers"></a>保护 SQL Server Docker 容器

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

默认情况下，SQL Server 2017 容器以根用户身份启动。 这可能会导致一些安全问题。 本文介绍了在运行 SQL Server Docker 容器时具有的安全选项，以及如何以非根用户身份生成 SQL Server 容器。

## <a name="build-and-run-non-root-sql-server-2017-containers"></a><a id="buildnonrootcontainer"></a> 生成并运行非根 SQL Server 2017 容器

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

    ```bash
    docker exec -it sql1 bash
    ```

    运行 `whoami`，这将返回容器中运行的用户。
    
    ```bash
    whoami
    ```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a>在主机上以其他非根用户的身份运行容器

若要以其他非根用户的身份运行 SQL Server 容器，请将 -u 标志添加到 docker run 命令。 非根容器具有以下限制：必须作为根组的一部分运行，除非已将卷装载到非根用户可以访问的 `/var/opt/mssql`。 根组不向非根用户授予任何额外的根权限。

#### <a name="run-as-a-user-with-a-uid-4000"></a>以具有 UID 4000 的用户身份运行

可使用自定义 UID 启动 SQL Server。 例如，以下命令使用 UID 4000 启动 SQL Server：

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> 确保 SQL Server 容器具有命名用户，如“mssql”或“root”，否则 SQLCMD 将无法在容器中运行。 可通过在容器中运行 `whoami` 来检查是否以命名用户的身份运行 SQL Server 容器。

#### <a name="run-the-non-root-container-as-the-root-user"></a>以根用户的身份运行非根容器

如果需要，可以根用户的身份运行非根容器。 这还会将所有文件权限自动授予容器，因为容器具有更高的特权。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-user-on-your-host-machine"></a>在主机计算机上以用户的身份运行

可使用以下命令在主机计算机上以现有用户身份启动 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-different-user-and-group"></a>以其他用户和组的身份运行

可使用自定义用户和组启动 SQL Server。 在此示例中，已装载的卷具有为主机计算机上的用户或组配置的权限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a>为非根容器配置持久存储权限

若要允许非根用户访问已装载卷上的数据库文件，请确保以可读取/写入持久文件存储的用户身份或组成员身份运行容器。  

可通过此命令获取数据库文件的当前所有权。

```bash
ls -ll <database file dir>
```

如果 SQL Server 无权访问持久数据库文件，请运行以下命令之一。

#### <a name="grant-the-root-group-rw-access-to-the-db-files"></a>授予对 DB 文件的根组读/写访问权限

授予对以下目录的根组权限，使非根 SQL Server 容器有权访问数据库文件。

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

#### <a name="set-the-non-root-user-as-the-owner-of-the-files"></a>将非根用户设置为文件的所有者

这可以是默认的非根用户，也可以是要指定的任何其他非根用户。 在此示例中，我们将 UID 10001 设置为非根用户。

```bash
chown -R 10001:0 <database file dir>
```

## <a name="next-steps"></a>后续步骤

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- 通过查看[快速入门](quickstart-install-connect-docker.md?view=sql-server-2017)，开始在 Docker 上使用 SQL Server 2017 容器映像

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- 通过查看[快速入门](quickstart-install-connect-docker.md?view=sql-server-ver15)，开始在 Docker 上使用 SQL Server 2019 容器映像

::: moniker-end

- [部署并连接到 SQL Server Docker 容器](sql-server-linux-docker-container-deployment.md)

- [引用 Docker 容器的其他配置和自定义](sql-server-linux-docker-container-configure.md)

- [SQL Server Docker 容器故障排除](sql-server-linux-docker-container-troubleshooting.md)