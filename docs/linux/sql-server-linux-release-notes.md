---
title: 有关在 Linux 上的 SQL Server 2017 发行说明 |Microsoft 文档
description: 本文包含的发行说明，并支持在 Linux 上运行的 SQL Server 2017 的功能。 发行说明也包括针对最新版本和多个以前的版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: b89daab4515e3017aa6e80f462e54020caf4ff91
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的发行说明

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下发行说明适用于 Linux 上运行的 SQL Server 2017。 本文分为每个版本的部分。 GA 版具有详细可支持性和已知问题列表。 每个累积更新 (CU) 版本具有描述 CU 更改以及指向包下载的 Linux 支持文章的链接。

## <a name="supported-platforms"></a>支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 或 7.4 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 有关详细信息，查看[系统要求](sql-server-linux-setup.md#system)在 Linux 上的 SQL server。 SQL Server 自 2017 年的最新支持策略，请参阅[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

目标 SQL Server 的大多数现有的客户端工具可无缝地将目标在 Linux 上运行的 SQL Server。 一些工具可能具有适用于 Linux 的特定版本要求。 SQL Server 工具的完整列表，请参阅[SQL 工具和 SQL Server 实用工具中的](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本历史记录

下表列出 SQL Server 自 2017 年发布历史记录。

| 发行版本 | 版本 | 发布日期 |
|-----|-----|-----|
| [CU6](#CU6) | 14.0.3025.34 | 4 2018 |
| [CU5](#CU5) | 14.0.3023.8 | 3 2018 |
| [CU4](#CU4) | 14.0.3022.28 | 2 2018 |
| [CU3](#CU3) | 14.0.3015.40 | 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a> 如何安装累积更新

如果你配置了累积更新存储库，然后将执行新安装时获取最新的累积 SQL Server 包更新。 在 Linux 上的 SQL Server 的所有包安装项目默认值为累积更新存储库。 有关存储库配置的详细信息，请参阅[为在 Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

如果你要更新现有的 SQL Server 包，运行每个包以便获取最新的累积更新的相应更新命令。 有关特定更新每个包的说明，请参阅以下安装指南：

- [安装 SQL Server 包](sql-server-linux-setup.md#upgrade)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [启用 SQL Server 代理](sql-server-linux-setup-sql-agent.md)

## <a id="CU6"></a> CU6 (年 4 月 2018)

这是 SQL Server 自 2017 年的累积更新 6 (CU6) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3025.34。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3025.34-3 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3025.34-3 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3025.34-3 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (年 3 月 2018)

这是 SQL Server 自 2017 年的累积更新 5 (CU5) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3023.8。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643)。

### <a name="known-upgrade-issue"></a>已知升级问题

当从以前的版本升级到 CU5 时，SQL Server 可能无法启动并出现以下错误：

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

若要解决此错误，启用 SQL Server 代理，并使用以下命令重新启动 SQL Server:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3023.8-5 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3023.8-5 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3023.8-5 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (年 2 月 2018)

这是 SQL Server 自 2017 年的累积更新 4 (CU4) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3022.28。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/en-us/help/4056498 ](https://support.microsoft.com/en-us/help/4056498)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

> [!NOTE]
> 截至 CU4，作为一个单独的包不再安装 SQL Server 代理。 它与引擎包安装，而必须启用才能使用。

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3022.28-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3022.28-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3022.28-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> CU3 (年 1 月 2018)

这是 SQL Server 自 2017 年的累积更新 3 (CU3) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3015.40。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/en-us/help/4052987 ](https://support.microsoft.com/en-us/help/4052987)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3015.40-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3015.40-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3015.40-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (自 2017 年 11 月)

这是 SQL Server 自 2017 年的累积更新 2 (CU2) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3008.27。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3008.27-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3008.27-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3008.27-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (自 2017 年 10 月)

这是 SQL Server 自 2017 年的累积更新 1 (CU1) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.3006.16。 有关修补程序和此版本中的改进的信息，请参阅[ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，你可以下载的 RPM 包和 Debian 包使用下表中的信息：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3006.16-3 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3006.16-3 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3006.16-3 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (自 2017 年 10 月)

这是正式版 (GA) 版本的 SQL Server 自 2017 年。 对于此版本的 SQL Server 引擎版本是 14.0.1000.169。

### <a name="package-details"></a>包详细信息

下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.1000.169-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.1000.169-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.1000.169-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 不支持的功能和服务

以下功能和服务在 GA 发行时不可用在 Linux 上。 将随着时间的推移越来越多地启用这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 事务复制 |
| &nbsp; | 合并复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 与第三方连接的分布式的查询 |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable，FILESTREAM |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| &nbsp; | 缓冲池扩展 |
| **SQL Server 代理** |  子系统： CmdExec、 PowerShell、 队列读取器、 SSIS、 SSAS、 SSRS |
| &nbsp; | 警报 |
| &nbsp; | 日志读取器代理 |
| &nbsp; | 变更数据捕获 |
| &nbsp; | 托管备份 |
| **高可用性** | 数据库镜像  |
| **安全性** | 可扩展的密钥管理 |
| &nbsp; | 对于链接服务器的 AD 身份验证 | 
| &nbsp; | 可用性组 （承载个可用性组） 的的 AD 身份验证 | 
| &nbsp; | 第三方 AD 工具 (Centrify，Vintela，Powerbroker) | 
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | “数据库引擎服务” |
| &nbsp; | Master Data Services |
| &nbsp; | 分布式的事务处理协调器 (DTC) |

## <a name="known-issues"></a>已知问题

下列各节描述在 Linux 上的 SQL Server 2017 正式版 (GA) 发布的已知的问题。

#### <a name="general"></a>常规

- 只能从 CTP 2.1 或更高版本支持升级到 GA 版本的 SQL Server 自 2017 年。 

- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- 默认语言**sa**登录名是英语。

    - **解析**： 更改的语言**sa**具有登录名**ALTER LOGIN**语句。

#### <a name="databases"></a>“数据库”

- 不能使用 mssql conf 实用工具移动 master 数据库。 可以使用 mssql 联赛移动其他系统数据库

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 SQL Server 到 SQL Server，除非它们涉及 DTC 支持链接的服务器。 有关详细信息，请参阅[在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)。

- 某些算法 （密码套件） 用于传输层安全性 (TLS) 与在 Linux 上的 SQL Server 工作不正常。 这会导致连接失败后尝试连接到 SQL Server，以及建立高可用性组中的副本之间的连接的问题。

   - **解析**： 修改**mssql.conf**通过执行以下操作来禁用有问题的密码套件，Linux 上的 SQL Server 的配置脚本：

      1. 将以下代码添加到 /var/opt/mssql/mssql.conf。

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 使用以下命令重新启动 SQL Server。

      ```bash
      sudo systemctl restart mssql-server
      ```

- 使用内存中 OLTP 的 Windows 上的 SQL Server 2014 数据库无法还原在 Linux 上的 SQL Server 2017 上。 若要还原使用内存中 OLTP 的 SQL Server 2014 数据库，首先将数据库升级到 SQL Server 2016 或 Windows 上的 SQL Server 2017 之前将其移动到 SQL Server 在 Linux 上通过备份/还原或分离/附加。

- 用户权限**ADMINISTER BULK OPERATIONS**不支持在 Linux 上这次。

#### <a name="networking"></a>网络

如果满足以下条件，涉及从 sqlservr 进程，如链接的服务器或可用性组的出站 TCP 连接的功能可能不起作用：

1. 目标服务器指定为主机名而不是 IP 地址。

1. 源实例已在内核中禁用 IPv6。 若要验证你的系统是否有在内核中启用了 IPv6，必须传递所有以下测试：

   - `cat /proc/cmdline` 将打印当前内核启动命令行。 输出不能包含`ipv6.disable=1`。
   - / 进程/sys/网络/ipv6/目录必须存在。
   - C 程序中调用`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`应成功-syscall 必须返回 fd ！ =-1 并不会因 EAFNOSUPPORT 失败。

具体错误取决于该功能。 对于链接服务器，这种情况登录超时错误。 对于可用性组， `ALTER AVAILABILITY GROUP JOIN` DDL 辅助副本上的将在 5 分钟下载配置超时错误后失败。

若要解决此问题，请执行以下操作：

1. 使用而不是主机名 Ip 指定 TCP 连接的目标。

1. 通过删除启用在内核中的 IPv6`ipv6.disable=1`从启动命令行。 若要执行此操作的方式取决于 Linux 分发和引导加载程序，如 grub。 如果你确实想要禁用的 IPv6，你仍然可以禁用它通过设置`net.ipv6.conf.all.disable_ipv6 = 1`中`sysctl`配置 (例如`/etc/sysctl.conf`)。 这仍将防止系统的网络适配器 IPv6 地址，但允许 sqlservr 功能工作。

#### <a name="network-file-system-nfs"></a>网络文件系统 (NFS)
如果你使用**网络文件系统 (NFS)** 在生产中的远程共享，请注意以下支持要求：

- 使用 NFS 版本**4.2 或更高版本**。 NFS 的较旧版本不支持所需的功能，如 fallocate 和稀疏文件创建，普遍适用于现代文件系统。
- 仅查找 **/var/opt/mssql**上 NFS 装入的目录。 其他文件，如 SQL Server 系统二进制文件，不支持。
- 确保安装对远程共享时，NFS 客户端，使用 nolock 选项。

#### <a name="localization"></a>本地化

- 如果你的区域设置不是在安装过程英语 (en_us)，则必须使用 utf-8 编码在 bash 会话/终端。 如果你使用 ASCII 编码，可能会看到如下错误：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果你不能使用 utf-8 编码，运行安装程序使用 MSSQL_LCID 环境变量来指定语言选择。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 如果运行 mssql conf 安装程序，并执行 SQL Server，不正确的非英语安装扩展字符将显示在本地化文本，"配置 SQL Server …"之后。 或者，对于非拉丁基于安装，可能是缺少句子完全。 缺少句子应显示以下的本地化的字符串:"已成功处理的授权 PID。  新的版本是 [\<名称\>版本]"。 此字符串输出信息仅用于，和下一步的 SQL Server 累积更新将解决此问题为所有语言。 这不会影响 SQL server 安装以任何方式成功。 

#### <a name="full-text-search"></a>全文搜索

- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- **Mssql 服务器是**包在此版本中不支持在 SUSE 上。 当前支持在 Ubuntu 上和 Red Hat Enterprise Linux (RHEL) 上。

- 借助上 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能已测试 SQL Server 和 MySQL ODBC 驱动程序，但还需要使用任何 Unicode ODBC 驱动程序观察到 ODBC 规范。 在设计时，你可以提供一个 DSN 或连接字符串以连接到 ODBC 数据中;你还可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 在 Linux 上运行 SSIS 包时，在此版本中不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - SSIS 横向扩展
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

有关内置 SSIS 组件当前不支持，或支持有限制的列表，请参阅[的限制和已知的问题在 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md#components)。

有关在 Linux 上的 SSIS 的详细信息，请参阅以下文章：
-   [博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 若要保留的日志文件数不能修改。

## <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [运行和连接 - 云](quickstart-install-connect-clouds.md)

有关的常见问题的答案，请参阅[Linux 常见问题的 SQL Server](sql-server-linux-faq.md)。
