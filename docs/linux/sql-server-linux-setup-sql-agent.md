---
title: 在 Linux 上安装 SQL Server 代理
description: 本文介绍如何在 Linux 上安装 SQL Server 代理。
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: c27a31a5e6b9ed771df82e942087d7be88270038
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032469"
---
# <a name="install-sql-server-agent-on-linux"></a>在 Linux 上安装 SQL Server 代理

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 [SQL Server 代理](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)运行计划的 SQL Server 作业。 从 SQL Server 2017 CU4 开始，SQL Server 代理包含在“mssql 服务器”包中，默认情况下处于禁用状态  。 若要了解此版本 SQL Server 代理支持的功能和版本信息，请参阅[发行说明](sql-server-linux-release-notes.md)。

 安装/启用 SQL Server 代理：
- [对于版本 2017 CU4 及更高版本，请启用 SQL Server 代理](#EnableAgentAfterCU4)
- [对于版本 2017 CU3 及更低版本，请安装 SQL Server 代理](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">对于版本 2017 CU4 及更高版本，请启用 SQL Server 代理</a>

 若要启用 SQL Server 代理，请执行以下步骤。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 如果是在安装了代理的情况下从 2017 CU3 或更低版本进行升级，将自动启用 SQL Server 代理并卸载以前的代理包。  

## <a name="InstallAgentBelowCU4">对于版本 2017 CU3 及更低版本，请安装 SQL Server 代理</a>

> [!NOTE]
> 下面的安装说明适用于 SQL Server 版本 2017 CU3 及更低版本。 在安装 SQL Server 代理前，首先请[安装 SQL Server](sql-server-linux-setup.md#platforms)。 这将配置安装 mssql-server-agent 包时要用到的密钥和存储库  。

为以下平台安装 SQL Server 代理：
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">在 RHEL 上安装</a>

通过下列步骤在 Red Hat Enterprise Linux 上安装 mssql-server-agent  。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已安装 mssql-server-agent，则可使用下列命令将其更新至最新版本  ：

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，请在[发行说明](sql-server-linux-release-notes.md)中找到 SQL Server 代理包下载。 然后执行与文章[安装 SQL Server](sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。

### <a name="ubuntu">在 Ubuntu 上安装</a>

通过下列步骤在 Ubuntu 上安装 mssql-server-agent  。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已安装 mssql-server-agent，则可使用下列命令将其更新至最新版本  ：

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，请在[发行说明](sql-server-linux-release-notes.md)中找到 SQL Server 代理包下载。 然后执行与文章[安装 SQL Server](sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。

### <a name="SLES">在 SLES 上安装</a>

通过下列步骤在 SUSE Linux Enterprise Server 上安装 mssql-server-agent  。 

安装 mssql-server-agent  

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已安装 mssql-server-agent，则可使用下列命令将其更新至最新版本  ：

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，请在[发行说明](sql-server-linux-release-notes.md)中找到 SQL Server 代理包下载。 然后执行与文章[安装 SQL Server](sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。

## <a name="next-steps"></a>后续步骤
有关如何使用 SQL Server 代理创建、计划和运行作业的详细信息，请参阅[在 Linux 上运行 SQL Server 代理作业](sql-server-linux-run-sql-server-agent-job.md)。
