---
title: 用环境变量配置 SQL Server 设置
description: 本文介绍如何使用环境变量在 Linux 上配置特定 SQL Server 2017 设置。
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419246"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>在 Linux 上使用环境变量配置 SQL Server 设置

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

可以使用多个不同的环境变量来配置 Linux 上的 SQL Server 2017。 在两个方案中使用这些变量:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

可以使用多个不同的环境变量在 Linux 上配置 SQL Server 2019 preview。 在两个方案中使用这些变量:

::: moniker-end

- 用`mssql-conf setup`命令配置初始设置。
- [在 Docker 中](quickstart-install-connect-docker.md)配置新的 SQL Server 容器。

> [!TIP]
> 如果需要在这些设置方案之后配置 SQL Server, 请参阅[配置 Linux 上的 SQL Server 与 mssql-会议工具](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>环境变量

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 环境变量 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 将 **ACCEPT_EULA** 变量设置为任意值，以确认接受[最终用户许可协议](https://go.microsoft.com/fwlink/?LinkId=746388)。 SQL Server 映像的必需设置。 |
| **MSSQL_SA_PASSWORD** | 配置 SA 用户密码。 |
| **MSSQL_PID** | 设置 SQL Server 版本或产品密钥。 可能的值包括： </br></br>**Evaluation**</br>**开发人员**</br>**Express**</br>**Web**</br>**Standard**</br>**版**</br>**产品密钥**</br></br>如果指定产品密钥, 则其格式必须为 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, 其中 "#" 是数字或字母。|
| **MSSQL_LCID** | 设置要用于 SQL Server 的语言 ID。 例如, 1036 为法语。 |
| **MSSQL_COLLATION** | 设置 SQL Server 的默认排序规则。 这将覆盖语言 id (LCID) 到排序规则的默认映射。 |
| **MSSQL_MEMORY_LIMIT_MB** | 设置 SQL Server 可以使用的最大内存量 (以 MB 为单位)。 默认情况下, 它是总物理内存的 80%。 |
| **MSSQL_TCP_PORT** | 配置 SQL Server 用于侦听的 TCP 端口（默认为 1433）。 |
| **MSSQL_IP_ADDRESS** | 设置 IP 地址。 目前，IP 地址必须为 IPv4 样式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 设置默认备份目录位置。 |
| **MSSQL_DATA_DIR** | 更改创建新 SQL Server 数据库数据文件 (.mdf) 的目录。 |
| **MSSQL_LOG_DIR** | 更改在其中创建新 SQL Server 数据库日志文件 (.ldf) 的目录。 |
| **MSSQL_DUMP_DIR** | 更改 SQL Server 存放内存转储和其他故障排除文件的默认目录。 |
| **MSSQL_ENABLE_HADR** | 启用可用性组。 例如, 启用 "1", 并禁用 "0" |
| **MSSQL_AGENT_ENABLED** | 启用 SQL Server 代理。 例如, 启用 "true", 禁用 "false"。 默认情况下, 代理处于禁用状态。  |
| **MSSQL_MASTER_DATA_FILE** | 设置 master 数据库数据文件的位置。 必须先命名为 **.master** , 才能开始 SQL Server 首次运行。 |
| **MSSQL_MASTER_LOG_FILE** | 设置 master 数据库日志文件的位置。 在 SQL Server 首次运行之前, 必须将其命名为**mastlog.ldf。** |
| **MSSQL_ERROR_LOG_FILE** | 设置错误日志文件的位置。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 环境变量 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 将 **ACCEPT_EULA** 变量设置为任意值，以确认接受[最终用户许可协议](https://go.microsoft.com/fwlink/?LinkId=746388)。 SQL Server 映像的必需设置。 |
| **MSSQL_SA_PASSWORD** | 配置 SA 用户密码。 |
| **MSSQL_PID** | 设置 SQL Server 版本或产品密钥。 可能的值包括： </br></br>**Evaluation**</br>**开发人员**</br>**Express**</br>**Web**</br>**Standard**</br>**版**</br>**产品密钥**</br></br>如果指定产品密钥, 则其格式必须为 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, 其中 "#" 是数字或字母。|
| **MSSQL_LCID** | 设置要用于 SQL Server 的语言 ID。 例如, 1036 为法语。 |
| **MSSQL_COLLATION** | 设置 SQL Server 的默认排序规则。 这将覆盖语言 id (LCID) 到排序规则的默认映射。 |
| **MSSQL_MEMORY_LIMIT_MB** | 设置 SQL Server 可以使用的最大内存量 (以 MB 为单位)。 默认情况下, 它是总物理内存的 80%。 |
| **MSSQL_TCP_PORT** | 配置 SQL Server 用于侦听的 TCP 端口（默认为 1433）。 |
| **MSSQL_IP_ADDRESS** | 设置 IP 地址。 目前，IP 地址必须为 IPv4 样式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 设置默认备份目录位置。 |
| **MSSQL_DATA_DIR** | 更改创建新 SQL Server 数据库数据文件 (.mdf) 的目录。 |
| **MSSQL_LOG_DIR** | 更改在其中创建新 SQL Server 数据库日志文件 (.ldf) 的目录。 |
| **MSSQL_DUMP_DIR** | 更改 SQL Server 存放内存转储和其他故障排除文件的默认目录。 |
| **MSSQL_ENABLE_HADR** | 启用可用性组。 例如, 启用 "1", 并禁用 "0" |
| **MSSQL_AGENT_ENABLED** | 启用 SQL Server 代理。 例如, 启用 "true", 禁用 "false"。 默认情况下, 代理处于禁用状态。  |
| **MSSQL_MASTER_DATA_FILE** | 设置 master 数据库数据文件的位置。 必须先命名为 **.master** , 才能开始 SQL Server 首次运行。 |
| **MSSQL_MASTER_LOG_FILE** | 设置 master 数据库日志文件的位置。 在 SQL Server 首次运行之前, 必须将其命名为**mastlog.ldf。** |
| **MSSQL_ERROR_LOG_FILE** | 设置错误日志文件的位置。 |

::: moniker-end

## <a name="use-with-initial-setup"></a>与初始设置一起使用

此示例与`mssql-conf setup`已配置的环境变量一起运行。 指定以下环境变量:

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**为非生产用途指定 SQL Server 自由许可的开发人员版本。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 在1234上进行侦听的 TCP 端口。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>与 Docker 一起使用

此示例 docker 命令使用以下环境变量来创建新的 SQL Server 容器:

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**为非生产用途指定 SQL Server 自由许可的开发人员版本。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 在1234上进行侦听的 TCP 端口。 这意味着, 在此示例中, 必须使用`-p 1234:1234`命令映射自定义 TCP 端口, 而不是将端口 1433 (默认值) 映射到主机端口。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

如果在 Linux/macOS 上运行 Docker, 请将以下语法与单引号一起使用:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

如果在 Windows 上运行 Docker, 请将以下语法与双引号一起使用:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 在容器中运行生产版本的过程略有不同。 有关详细信息，请参阅[运行生产容器映像](sql-server-linux-configure-docker.md#production)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

如果在 Linux/macOS 上运行 Docker, 请将以下语法与单引号一起使用:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

如果在 Windows 上运行 Docker, 请将以下语法与双引号一起使用:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>后续步骤

有关此处未列出的其他 SQL Server 设置, 请参阅[通过 mssql 会议工具配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)。

有关如何安装和运行 Linux 上的 SQL Server 的详细信息, 请参阅[安装 Linux 上的 SQL Server](sql-server-linux-setup.md)。
