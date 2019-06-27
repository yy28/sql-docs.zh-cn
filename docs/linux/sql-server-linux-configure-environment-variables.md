---
title: 使用环境变量配置 SQL Server 设置 |Microsoft Docs
description: 本文介绍如何使用环境变量在 Linux 上配置 SQL Server 2017 的特定设置。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 2b32c965dfed3647484a1de54539c79af3777ce4
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400073"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>在 Linux 上使用环境变量配置 SQL Server 设置

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

多个不同的环境变量可用于在 Linux 上配置 SQL Server 2017。 两个方案中使用这些变量：

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

多个不同的环境变量可用于在 Linux 上配置 SQL Server 2019 预览。 两个方案中使用这些变量：

::: moniker-end

- 若要配置与初始设置`mssql-conf setup`命令。
- 若要配置一个新[SQL Server 容器在 Docker 中的](quickstart-install-connect-docker.md)。

> [!TIP]
> 如果需要将 SQL Server 配置这些设置方案后，请参阅[在 Linux 上使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>环境变量

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 环境变量 | Description |
|-----|-----|
| **ACCEPT_EULA** | 在设置为任何值（例如“Y”）时接受 SQL Server 许可协议。 |
| **MSSQL_SA_PASSWORD** | 配置 SA 用户密码。 |
| **MSSQL_PID** | 设置 SQL Server 版本或产品密钥。 可能的值包括： </br></br>**Evaluation**</br>**开发人员**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**产品密钥**</br></br>如果指定产品密钥，它必须是格式为 # # #-# # #-# # #-# # #-# # #，其中 # 是数字或字母。|
| **MSSQL_LCID** | 设置要用于 SQL Server 的语言 ID。 例如 1036年为法语。 |
| **MSSQL_COLLATION** | 设置 SQL Server 的默认排序规则。 这会重写排序规则的语言 id (LCID) 的默认的映射。 |
| **MSSQL_MEMORY_LIMIT_MB** | 设置 SQL Server 可使用的内存 （以 mb 为单位） 的最长。 默认情况下它是总物理内存的 80%。 |
| **MSSQL_TCP_PORT** | 配置 SQL Server 用于侦听的 TCP 端口（默认为 1433）。 |
| **MSSQL_IP_ADDRESS** | 设置 IP 地址。 目前，IP 地址必须为 IPv4 样式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 设置默认备份目录位置。 |
| **MSSQL_DATA_DIR** | 更改创建新 SQL Server 数据库数据文件 (.mdf) 的目录。 |
| **MSSQL_LOG_DIR** | 更改在其中创建新的 SQL Server 数据库日志 (.ldf) 文件的目录。 |
| **MSSQL_DUMP_DIR** | 更改 SQL Server 存放内存转储和其他故障排除文件的默认目录。 |
| **MSSQL_ENABLE_HADR** | 启用可用性组。 例如，"1"已启用，并禁用"0" |
| **MSSQL_AGENT_ENABLED** | 启用 SQL Server 代理。 例如，启用了 'true' 和 'false' 被禁用。 默认情况下禁用代理。  |
| **MSSQL_MASTER_DATA_FILE** | 设置 master 数据库数据文件的位置。 必须命名为**master.mdf**直到首次运行的 SQL Server。 |
| **MSSQL_MASTER_LOG_FILE** | 设置 master 数据库日志文件的位置。 必须命名为**mastlog.ldf**直到首次运行的 SQL Server。 |
| **MSSQL_ERROR_LOG_FILE** | 设置错误日志文件的位置。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 环境变量 | Description |
|-----|-----|
| **ACCEPT_EULA** | 在设置为任何值（例如“Y”）时接受 SQL Server 许可协议。 |
| **MSSQL_SA_PASSWORD** | 配置 SA 用户密码。 |
| **MSSQL_PID** | 设置 SQL Server 版本或产品密钥。 可能的值包括： </br></br>**Evaluation**</br>**开发人员**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**产品密钥**</br></br>如果指定产品密钥，它必须是格式为 # # #-# # #-# # #-# # #-# # #，其中 # 是数字或字母。|
| **MSSQL_LCID** | 设置要用于 SQL Server 的语言 ID。 例如 1036年为法语。 |
| **MSSQL_COLLATION** | 设置 SQL Server 的默认排序规则。 这会重写排序规则的语言 id (LCID) 的默认的映射。 |
| **MSSQL_MEMORY_LIMIT_MB** | 设置 SQL Server 可使用的内存 （以 mb 为单位） 的最长。 默认情况下它是总物理内存的 80%。 |
| **MSSQL_TCP_PORT** | 配置 SQL Server 用于侦听的 TCP 端口（默认为 1433）。 |
| **MSSQL_IP_ADDRESS** | 设置 IP 地址。 目前，IP 地址必须为 IPv4 样式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 设置默认备份目录位置。 |
| **MSSQL_DATA_DIR** | 更改创建新 SQL Server 数据库数据文件 (.mdf) 的目录。 |
| **MSSQL_LOG_DIR** | 更改在其中创建新的 SQL Server 数据库日志 (.ldf) 文件的目录。 |
| **MSSQL_DUMP_DIR** | 更改 SQL Server 存放内存转储和其他故障排除文件的默认目录。 |
| **MSSQL_ENABLE_HADR** | 启用可用性组。 例如，"1"已启用，并禁用"0" |
| **MSSQL_AGENT_ENABLED** | 启用 SQL Server 代理。 例如，启用了 'true' 和 'false' 被禁用。 默认情况下禁用代理。  |
| **MSSQL_MASTER_DATA_FILE** | 设置 master 数据库数据文件的位置。 必须命名为**master.mdf**直到首次运行的 SQL Server。 |
| **MSSQL_MASTER_LOG_FILE** | 设置 master 数据库日志文件的位置。 必须命名为**mastlog.ldf**直到首次运行的 SQL Server。 |
| **MSSQL_ERROR_LOG_FILE** | 设置错误日志文件的位置。 |

::: moniker-end

## <a name="use-with-initial-setup"></a>使用与初始设置

此示例将运行`mssql-conf setup`与已配置的环境变量。 指定以下环境变量：

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**指定免费许可开发人员版的 SQL Server 非生产环境中使用。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 学习 1234年侦听的 TCP 端口。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>与 Docker 一起使用

此示例 docker 命令使用以下环境变量来创建新的 SQL Server 容器：

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**指定免费许可开发人员版的 SQL Server 非生产环境中使用。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 学习 1234年侦听的 TCP 端口。 这意味着，而不是到主机端口映射端口 1433 （默认值），必须将自定义 TCP 端口映射与`-p 1234:1234`命令在此示例中。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

如果在 Linux/macOS 上运行 Docker，请用单引号使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

如果在 Windows 上运行 Docker，请用双引号引起来使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 在容器中运行生产版本的过程略有不同。 有关详细信息，请参阅[运行生产容器映像](sql-server-linux-configure-docker.md#production)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

如果在 Linux/macOS 上运行 Docker，请用单引号使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

如果在 Windows 上运行 Docker，请用双引号引起来使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>后续步骤

有关此处未列出其他 SQL Server 设置，请参阅[在 Linux 上使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

有关如何安装和 Linux 上运行 SQL Server 的详细信息，请参阅[Linux 上安装 SQL Server](sql-server-linux-setup.md)。
