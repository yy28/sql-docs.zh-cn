---
title: "使用环境变量配置 SQL Server 设置 |Microsoft 文档"
description: "本主题介绍如何使用环境变量来在 Linux 上配置特定的 SQL Server 2017 设置。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/21/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: 44c33e0f5619349dfa32b48d7745ae6f9ddcc155
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>在 Linux 上使用环境变量配置 SQL Server 设置

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

多个不同的环境变量可用于在 Linux 上配置 SQL Server 自 2017 年。 在两个方案中使用这些变量：

- 若要配置与初始设置`mssql-conf setup`命令。
- 若要配置新[在 Docker 中的 SQL Server 容器](quickstart-install-connect-docker.md)。

> [!TIP]
> 如果你需要将 SQL Server 配置在这些安装程序方案后，请参阅[使用 mssql conf 工具的 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>环境变量

| 环境变量 | Description |
|-----|-----|
| **ACCEPT_EULA** | 在设置为任何值（例如“Y”）时接受 SQL Server 许可协议。 |
| **MSSQL_SA_PASSWORD** | 配置 SA 用户密码。 |
| **MSSQL_PID** | 设置 SQL Server 版本或产品密钥。 可能的值包括： </br></br>**Evaluation**</br>**开发人员**</br>**速成版**</br>**Web**</br>**Standard**</br>**企业**</br>**产品密钥**</br></br>如果指定产品密钥，则它必须 # # #-# # #-# # #-# # #-# # #，其中 '#' 是一个数字或字母形式。|
| **MSSQL_LCID** | 设置要用于 SQL Server 的语言 ID。 例如 1036年为法语。 |
| **MSSQL_COLLATION** | 设置 SQL Server 的默认排序规则。 此设置将替代对排序规则的语言 id (LCID) 的默认映射。 |
| **MSSQL_MEMORY_LIMIT_MB** | 设置最大 （以 mb 为单位） 可以使用 SQL Server 的内存量。 默认情况下它为总物理内存的 80%。 |
| **MSSQL_TCP_PORT** | 配置 SQL Server 用于侦听的 TCP 端口（默认为 1433）。 |
| **MSSQL_IP_ADDRESS** | 设置 IP 地址。 目前，IP 地址必须为 IPv4 样式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 设置默认备份目录位置。 |
| **MSSQL_DATA_DIR** | 更改创建新 SQL Server 数据库数据文件 (.mdf) 的目录。 |
| **MSSQL_LOG_DIR** | 更改其中创建新的 SQL Server 数据库日志 (.ldf) 文件的目录。 |
| **MSSQL_DUMP_DIR** | 更改 SQL Server 存放内存转储和其他故障排除文件的默认目录。 |
| **MSSQL_ENABLE_HADR** | 启用可用性组。 |

## <a name="example-initial-setup"></a>示例： 初始设置

此示例将运行`mssql-conf setup`与配置环境变量。 指定以下环境变量：

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**指定自由许可开发人员版 SQL Server 的非生产环境中使用。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 学习 1234年侦听的 TCP 端口。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>示例： Docker

此示例 docker 命令使用以下环境变量来创建新的 SQL Server 2017 容器：

- **ACCEPT_EULA**接受最终用户许可协议。
- **MSSSQL_PID**指定自由许可开发人员版 SQL Server 的非生产环境中使用。
- **MSSQL_SA_PASSWORD**设置强密码。
- **MSSQL_TCP_PORT**设置 SQL Server 学习 1234年侦听的 TCP 端口。 这意味着，而不是主机端口映射端口 1433 （默认值），自定义的 TCP 端口必须使用映射`-p 1234:1234`命令在此示例中。

如果你在 Linux/macOS 上运行 Docker，请用单引号使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

如果你在 Windows 上运行 Docker，请用双引号使用以下语法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> 在容器中运行生产版本的过程是略有不同。 有关详细信息，请参阅[运行容器映像的生产](sql-server-linux-configure-docker.md#production)。

## <a name="next-steps"></a>后续步骤

未在此处列出的其他 SQL Server 设置，请参阅[使用 mssql conf 工具的 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

有关如何安装和运行在 Linux 上的 SQL Server 的详细信息，请参阅[在 Linux 上安装 SQL Server](sql-server-linux-setup.md)。
