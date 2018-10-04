---
title: 在 Linux 上安装 SQL Server 代理 |Microsoft Docs
description: 本文介绍如何在 Linux 上安装 SQL Server 代理。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 72a4242373af16ffcdc8f749b899747801d2002c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819515"
---
# <a name="install-sql-server-agent-on-linux"></a>在 Linux 上安装 SQL Server 代理

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 [SQL Server 代理](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)运行 SQL Server 的计划的作业。 从 SQL Server 2017 CU4 开始，SQL Server 代理是附带**mssql server**打包并默认处于禁用状态。 对于此版本的 SQL Server 代理的版本信息以及支持的功能的信息，请参阅[发行说明](sql-server-linux-release-notes.md)。

 安装/启用 SQL Server 代理：
- [有关版本 2017 CU4 和更高版本中，启用 SQL Server 代理](#EnableAgentAfterCU4)
- [有关版本 2017 CU3 和更低版本，安装 SQL Server 代理](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">有关版本 2017 CU4 和更高版本中，启用 SQL Server 代理</a>

 若要启用 SQL Server 代理，请执行以下步骤。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 如果要从 2017 CU3 升级或以下代理安装，SQL Server 代理将与已启用自动和上一个会卸载代理包。  

## <a name="InstallAgentBelowCU4">有关版本 2017 CU3 和更低版本，安装 SQL Server 代理</a>

> [!NOTE]
> 下面的说明安装适用于 SQL Server 版本 2017 CU3 和更。 首次安装 SQL Server 代理前[安装 SQL Server](sql-server-linux-setup.md#platforms)。 这会配置密钥和在安装时使用的存储库**mssql server 代理**包。

为以下平台安装 SQL Server 代理：
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">在 RHEL 上安装</a>

使用以下步骤来安装**mssql server 代理**Red Hat Enterprise Linux 上。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已有**mssql server 代理**安装，您可以更新最新版本使用以下命令：

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，找到 SQL Server 代理包下载[发行说明](sql-server-linux-release-notes.md)。 然后，使用本文所述相同的脱机安装步骤[安装 SQL Server](sql-server-linux-setup.md#offline)。

### <a name="ubuntu">在 Ubuntu 上安装</a>

使用以下步骤来安装**mssql server 代理**Ubuntu 上。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已有**mssql server 代理**安装，您可以更新最新版本使用以下命令：

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，找到 SQL Server 代理包下载[发行说明](sql-server-linux-release-notes.md)。 然后，使用本文所述相同的脱机安装步骤[安装 SQL Server](sql-server-linux-setup.md#offline)。

### <a name="SLES">在 SLES 上安装</a>

使用以下步骤来安装**mssql server 代理**SUSE Linux Enterprise Server 上。 

安装**mssql server 代理** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

如果已有**mssql server 代理**安装，您可以更新最新版本使用以下命令：

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

如果需要脱机安装，找到 SQL Server 代理包下载[发行说明](sql-server-linux-release-notes.md)。 然后，使用本文所述相同的脱机安装步骤[安装 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="next-steps"></a>后续步骤
有关如何使用 SQL Server 代理来创建、 安排和运行作业的详细信息，请参阅[在 Linux 上运行的 SQL Server 代理作业](sql-server-linux-run-sql-server-agent-job.md)。
