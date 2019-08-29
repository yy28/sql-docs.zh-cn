---
title: Linux 上的 SQL Server 2019 的发行说明
description: 本文包含 Linux 上运行的 SQL Server 2019 的发行说明和支持功能。 发行说明适用于最新版本和几个以前的版本。
author: VanMSFT
ms.author: vanto
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b6f82e3b76e2dd2b11403bccf4b3e0885912e
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890901"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Linux 上的 SQL Server 2019 的发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

以下发行说明适用于 Linux 上运行的 SQL Server 2019。 本文按各版本分为不同的部分。 每个版本都有介绍 CU 更改的支持性文章的链接，还有 Linux 包下载的链接。

> [!TIP]
> 若要了解 SQL Server 2019 中的新增 Linux 功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。

## <a name="supported-platforms"></a>支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、7.4、7.5 或7.6 服务器 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| 适用于 Windows、Mac 或 Linux 的 Docker 引擎 1.8 及更高版本 | 空值 | [安装指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 有关详细信息，请查看 Linux 上 SQL Server 的[系统要求](sql-server-linux-setup.md#system)。 有关 SQL Server 2017 的最新支持策略，请参阅 [Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

以 SQL Server 为目标的大多数现有客户端工具可无缝转为以 Linux 上运行的 SQL Server 为目标。 某些工具与 Linux 配合使用时可能有特定的版本要求。 有关 SQL Server 工具的完整列表，请参阅[适用于 SQL Server 的 SQL 工具和实用程序](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本历史记录

下表列出了 SQL Server 2019 预览版的发布历史记录。

| 发行版本                   | 版本       | 发布日期 |
|---------------------------|---------------|--------------|
| [候选发布](#rc)  | 15.0.1900.25  | 2019年 8 月 21 日    |
| [CTP 3.2](#CTP32)         | 15.0.1800.32  | 2019 年 7 月 24 日    |
| [CTP 3.1](#CTP31)         | 15.0.1700.37  | 2019 年 6 月 26日    |
| [CTP 3.0](#CTP30)         | 15.0.1600.8   | 2019 年 5 月 22 日    |
| [CTP 2.5](#CTP25)         | 15.0.1500.28  | 2019 年 4 月 24 日    |
| [CTP 2.4](#CTP24)         | 15.0.1400.75  | 2019 年 3 月 27 日    |
| [CTP 2.3](#CTP23)         | 15.0.1300.359 | 2019 年 3 月 1 日    |
| [CTP 2.2](#CTP22)         | 15.0.1200.24  | 2018 年 12 月 11日   |
| [CTP 2.1](#CTP21)         | 15.0.1100.94  | 2018 年 11 月 6 日   |
| [CTP 2.0](#CTP20)         | 15.0.1000.34  | 2018 年 9 月 24 日   |

## <a id="cuinstall"></a> 如何安装更新

如果已配置预览存储库 (mssql-server preview)，则在执行新安装时将获得最新的 SQL Server CTP 包  。 如果需要 Docker 容器映像，请参阅[适用于 Docker 引擎的 Linux 上的 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server/) 的官方映像。 有关存储库配置的详细信息，请参阅[在 Linux 上为 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

如果要更新现有的 SQL Server 包，请为每个包运行相应的更新命令以获取最新的 CU。 有关每个包的特定更新说明，请参阅以下安装指南：

- [安装 SQL Server 包](sql-server-linux-setup.md#upgrade)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [在 Linux 上安装 SQL Server 2019 预览版的 Microsoft 机器学习服务 R 和 Python 支持](sql-server-linux-setup-machine-learning.md)
- [安装 PolyBase 包](../relational-databases/polybase/polybase-linux-setup.md)
- [启用 SQL Server 代理](sql-server-linux-setup-sql-agent.md)

## <a id="rc"></a> 候选发布（2019 年 8 月）

下面几个部分介绍了候选发布的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1900.25-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1900.25-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1900.25-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1900.25-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[PolyBase RPM 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a id="CTP32"></a> CTP 3.2（2019 年 7 月）

以下各节提供了 CTP 3.2 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1800.32-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1800.32-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1800.32-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[PolyBase RPM 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1（2019 年 6 月）

以下各节提供了 CTP 3.1 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1700.37-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| SLES RPM 包 | 15.0.1700.37-2 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1700.37-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[PolyBase RPM 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0（2019 年 5 月）

以下各节提供了用于 CTP 3.0 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1600.8-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1600.8-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1600.8-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[PolyBase RPM 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP25"></a> CTP 2.5（2019 年 5 月）

以下各节提供了 CTP 2.5 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1500.28-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1500.28-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1500.28-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[PolyBase RPM 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP24"></a> CTP 2.4（2019 年 3 月）

以下各节提供了 CTP 2.4 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1400.75-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| SLES RPM 包 | 15.0.1400.75-2 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1400.75-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP23"></a> CTP 2.3（2019 年 2 月）

以下各节提供了 CTP 2.3 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1300.359-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1300.359-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1300.359-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP22"></a> CTP 2.2（2018 年 12 月）

以下各节提供了 CTP 2.2 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1200.24-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| SLES RPM 包 | 15.0.1200.24-2 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1200.24-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a id="msdtc"></a> Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP21"></a> CTP 2.1（2018 年 11 月）

以下各节提供了 CTP 2.1 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1100.94-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| SLES RPM 包 | 15.0.1100.94-1 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1100.94-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a id="CTP20"></a> CTP 2.0（2018 年 9 月）

以下各节提供了 CTP 2.0 版本的包位置和已知问题。 若要详细了解 SQL Server 2019 上 Linux 的新功能，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>包详细信息

对于手动安装或脱机包安装，可以下载 RPM 和 Debian 包，其信息如下表所示：

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 15.0.1000.34-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 包 | 15.0.1000.34-2 | [mssql-server 引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 扩展性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 包 | 15.0.1000.34-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 扩展性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>已知问题

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分布式事务处理协调器

目前，MSDTC 要求事务不经过身份验证。 例如，如果使用从 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的链接服务器，或者使用 Windows 客户端应用程序针对 Linux 上的 SQL Server 启动某个分布式事务，则 Windows 服务器/客户端上的 MSDTC 需要使用“无需身份验证”选项。

## <a name="next-steps"></a>后续步骤

要开始使用，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [运行和连接 - 云](quickstart-install-connect-clouds.md)

有关常见问题的解答，请参阅 [Linux 上的 SQL Server 常见问题解答](sql-server-linux-faq.md)。
