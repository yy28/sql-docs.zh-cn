---
title: Linux 上的 SQL Server 2019 预览版的发行说明 |Microsoft Docs
description: 本文包含的发行说明，并在 Linux 上运行的 SQL Server 2019 CTP 的支持的功能。 包含最新版本和多个以前版本的发行说明。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 54b955609941e1c4f5921486fc5c67716120a499
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049408"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Linux 上的 SQL Server 2019 预览版发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

以下发行说明适用于 Linux 上运行的 SQL Server 2019 CTP。 本文将划分成的部分，了解每个版本。 每个版本具有描述 CU 更改以及链接到包下载的 Linux 支持文章的链接。

> [!TIP]
> 若要了解有关 SQL Server 2019 中的新 Linux 功能，请参阅[什么是 SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sqllinux)。

## <a name="supported-platforms"></a>支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 或 7.4 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 详细信息，请查看[系统要求](sql-server-linux-setup.md#system)Linux 上的 SQL Server。 SQL Server 2017 的最新支持策略，请参阅[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

目标 SQL Server 的大多数现有的客户端工具可以无缝地面向 Linux 上运行的 SQL Server。 一些工具可能会有很好地配合 Linux 特定版本要求。 SQL Server 工具的完整列表，请参阅[SQL 工具和适用于 SQL Server 实用工具](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>发布历史记录

下表列出了 SQL Server 2019 Ctp 发行历史记录。

| 发行版本               | 版本       | 发布日期 |
|-----------------------|---------------|--------------|
| [CTP 2.0](#CTP20) | 15.0.1000.34   | 2018-09-24   |

## <a id="cuinstall"></a> 如何安装更新

如果已配置预览存储库 (**mssql server 预览版**)，然后执行全新安装时，您将看到最新的 SQL Server CTP 包。 如果您需要 Docker 容器映像，请参阅官方的映像[Docker 引擎的 Linux 上的 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server/)。 有关存储库配置的详细信息，请参阅[Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

如果要更新现有的 SQL Server 包，运行每个包，以获取最新 CU 的相应更新命令。 有关特定更新的每个包的说明，请参阅以下安装指南：

- [安装 SQL Server 包](sql-server-linux-setup.md#upgrade)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [在 Linux 上安装 SQL Server 2019 预览机器学习服务 R 和 Python 支持](sql-server-linux-setup-machine-learning.md)
- [启用 SQL Server 代理](sql-server-linux-setup-sql-agent.md)

## <a id="CTP20"></a> CTP 2.0 (2018 年 9 月)

以下部分提供了包位置和发布的 CTP 2.0 已知的问题。 若要了解适用于 Linux 上 SQL Server 2019 有关新功能的详细信息，请参阅[什么是 SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装，您可以下载与下表中的信息的 RPM 和 Debian 包：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1000.34-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[可扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 包 | 15.0.1000.34-2 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[可扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1000.34-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[可扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求为未经身份验证的事务。 例如，如果 Windows 到 Linux 上的 SQL Server 上使用从 SQL Server 的链接的服务器或使用 Windows 客户端应用程序在 Linux 上启动针对 SQL Server 的分布式的事务，Windows server/客户端上的 MSDTC 则需要为"不使用选项需要身份验证。

## <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [运行和连接 - 云](quickstart-install-connect-clouds.md)

有关常见问题的解答，请参阅[SQL Server Linux 常见问题](sql-server-linux-faq.md)。