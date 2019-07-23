---
title: Linux 版 SQL Server 2017 的发行说明
description: 本文包含 Linux 上运行的 SQL Server 2017 的发行说明和支持的功能。 发行说明适用于最新版本和几个以前的版本。
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388411"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的发行说明

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下发行说明适用[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]于在 Linux 上运行。 本文分为每个版本的各个部分。 GA 版具有详细可支持性和已知问题列表。 每个累积更新 (CU) 或常规分发版本 (GDR) 都包含一个链接, 该链接指向描述 CU 更改的支持文章和 Linux 包下载的链接。

> [!TIP]
> 这些发行说明专门用于[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]发布。 有关新[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]的详细信息, 请参阅[Linux 上的 SQL Server 2019 预览版的发行说明](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)。

## <a name="supported-platforms"></a>受支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、7.4、7.5 或7.6 服务器 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | 不可用 | [安装指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 有关详细信息, 请参阅 Linux [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上的[系统要求](sql-server-linux-setup.md#system)。 有关的最新支持策略[!INCLUDE[ssSQL17](../includes/sssql17-md.md)], 请参阅[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

大多数面向[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的现有客户端工具都可以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无缝地在 Linux 上运行。 某些工具可能具有特定版本要求, 可与 Linux 配合使用。 有关完整的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]工具列表, 请参阅[SQL Server 的 SQL 工具和实用工具](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>发布历史记录

下表列出了的发行历史记录[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。

| 发行版本               | Version       | 发布日期 |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a>如何安装更新

如果已配置 CU 存储库 (**mssql-server-2017**), 则在执行新安装时, 你将[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]获得最新的包 CU。 对于 Linux [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上的所有包安装文章, CU 存储库是默认值。 如果已配置 GDR 存储库 (**mssql-server-2017-gdr**), 则只会获得公开上市以来发布的关键安全更新。 如果需要 Docker 容器 CU 或 GDR 更新, 请参阅适用[于 Docker 引擎 Linux 上的 Microsoft SQL Server 的](https://hub.docker.com/r/microsoft/mssql-server)官方映像。 有关存储库配置的详细信息, 请参阅[为 Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

如果要更新现有[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]包, 请对每个包运行相应的 update 命令, 以获取最新的 CU。 有关每个包的特定更新说明, 请参阅以下安装指南:

- [安装 SQL Server 包](sql-server-linux-setup.md#upgrade)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [启用 SQL Server 代理](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a>CU15 (可能为 2019)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 15 (CU15) 版本。 此版本的版本为14.0.3162.1。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3162.1-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3162.1-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3162.1-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a>CU14 (三月 2019)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 14 (CU14) 版本。 此版本的版本为14.0.3076.1。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3076.1-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3076.1-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3076.1-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a>CU13 (2018 年12月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 13 (CU13) 版本。 此版本的版本为14.0.3048.4。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3048.4-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3048.4-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3048.4-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a>CU12 (10 月 2018)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 12 (CU12) 版本。 此版本的版本为14.0.3045.24。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3045.24-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3045.24-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3045.24-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a>CU11 (九月2018年9月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 11 (CU11) 版本。 此版本的版本为14.0.3038.14。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3038.14-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3038.14-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3038.14-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a>CU10 (2018 年8月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 10 (CU10) 版本。 此版本的版本为14.0.3037.1。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3037.1-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3037.1-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3037.1-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a>CU9-GDR2 (2018 年8月)

这是一个安全更新, 还包括以前发布的 CU (CU9) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 此版本的版本为14.0.3035.2。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3035.2-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 包 | 14.0.3035.2-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3035.2-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a>GDR2 (2018 年8月)

这是一个安全更新, 只包括的 GDR2 (和 GDR1) 安全修补程序[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。  此版本的版本为14.0.2002.14。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.2002.14-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.2002.14-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.2002.14-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a>CU9 (2018 年7月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 9 (CU9) 版本。 此版本的版本为14.0.3030.27。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3030.27-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3030.27-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3030.27-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a>CU8 (2018 年6月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 8 (CU8) 版本。 此版本的版本为14.0.3029.16。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3029.16-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3029.16-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3029.16-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a>CU7 (可能为 2018)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 7 (CU7) 版本。 此版本的版本为14.0.3026.27。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3026.27-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3026.27-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3026.27-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a>CU6 (四月 2018)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 6 (CU6) 版本。 此版本的版本为14.0.3025.34。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3025.34-3 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3025.34-3 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3025.34-3 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a>CU5 (三月 2018)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 5 (CU5) 版本。 此版本的版本为14.0.3023.8。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)参阅。

### <a name="known-upgrade-issue"></a>已知升级问题

从以前的版本升级到 CU5 时, 可能[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无法启动, 并出现以下错误:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

若要解决此错误, 请使用以下[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]命令启用 SQL Server 代理和重新启动:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3023.8-5 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3023.8-5 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3023.8-5 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a>CU4 (2018 年2月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 4 (CU4) 版本。 此版本的版本为14.0.3022.28。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

> [!NOTE]
> 在 CU4 中, SQL Server 代理不再作为单独的包安装。 它与引擎包一起安装, 必须启用才能使用。

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3022.28-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3022.28-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3022.28-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a>GDR1 (2018 年1月)

这是一个安全更新, 只包括的 GDR1 安全修补程序[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 此版本的版本为14.0.2000.63。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.2000.63-3 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 包 | 14.0.2000.63-3 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.2000.63-3 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a>CU3 (2018 年1月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 3 (CU3) 版本。 此版本的版本为14.0.3015.40。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3015.40-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3015.40-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3015.40-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a>CU2 (2017 年11月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 2 (CU2) 版本。 此版本的版本为14.0.3008.27。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3008.27-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3008.27-1 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3008.27-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a>CU1 (10 月 2017)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]累积更新 1 (CU1) 版本。 此版本的版本为14.0.3006.16。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 有关此版本中的修复和改进的信息, 请[https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)参阅。

### <a name="package-details"></a>包详细信息

对于手动或脱机包安装, 你可以下载 RPM 和 Debian 包, 其中包含下表中的信息:

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.3006.16-3 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.3006.16-3 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.3006.16-3 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (2017 年10月)

这是的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]公开发布 (GA) 版本。 此版本的版本为14.0.1000.169。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]

### <a name="package-details"></a>包详细信息

下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)
- [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| package | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.1000.169-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.1000.169-2 | [mssql-服务器引擎 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.1000.169-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a>服务 & 不支持的功能

公开发布时, Linux 上不提供以下功能和服务。 随着时间的推移, 支持这些功能会越来越多。

| 区域 | 不受支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 事务复制 |
| &nbsp; | 合并复制 |
| &nbsp; | 变更数据捕获 (请参阅 SQL Server 代理) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | 具有第三方连接的分布式查询 |
| &nbsp; | 除以外的其他数据源的链接服务器[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| &nbsp; | 缓冲池扩展 |
| **SQL Server 代理** |  子系统CmdExec、PowerShell、队列读取器、SSIS、SSAS、SSRS |
| &nbsp; | 警报 |
| &nbsp; | 日志读取器代理 |
| &nbsp; | 变更数据捕获 (CDC) |
| &nbsp; | 托管备份 |
| **高可用性** | 数据库镜像  |
| **安全性** | 可扩展的密钥管理 |
| &nbsp; | 链接服务器的 AD 身份验证 | 
| &nbsp; | 针对可用性组的 AD 身份验证 (Ag) | 
| &nbsp; | 第三方 AD 工具 (Centrify、Vintela、Powerbroker) | 
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | “数据库引擎服务” |
| &nbsp; | Master Data Services |
| &nbsp; | 分布式事务处理协调器 (DTC) |

## <a name="known-issues"></a>已知问题

以下部分介绍 Linux 上的公开上市 (GA) 版本的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]已知问题。

#### <a name="general"></a>常规

- 安装的主机名[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的长度必须小于或等于15个字符。 

    - **解决方法**:将/etc/hostname 中的名称更改为大于或等于15个字符。

- 手动将系统时间设置为 "及时" 将[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]导致停止更新内[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的内部系统时间。

    - **解决方法**:重新启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

- 仅支持单个实例安装。

    - **解决方法**:如果希望在给定主机上具有多个实例, 请考虑使用 Vm 或 Docker 容器。 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager 无法连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux 上的。

- **Sa**登录名的默认语言为英语。

    - **解决方法**:通过**ALTER login**语句更改**sa**登录名的语言。

#### <a name="databases"></a>数据库

- 不能将 master 数据库与 mssql 会议实用工具一起移动。 其他系统数据库可以通过 mssql 会议进行移动。

- 还原在 Windows 上备份[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的数据库时, 必须在 transact-sql 语句中使用**WITH MOVE**子句。

- 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux 上运行时, 不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]链接服务器, 除非它们涉及 DTC。 有关详细信息, 请参阅[在 Linux 上运行 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)。

- 传输层安全性 (TLS) 的某些算法 (密码套件) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上无法正常工作。 这会导致在尝试连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时连接失败, 以及在高可用性组中的副本之间建立连接时出现问题。

   - **解决方法**:通过执行  以下操作, 修改 Linux 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的 mssql 的配置脚本以禁用有问题的密码套件:

      1. 将以下项添加到/var/opt/mssql/mssql.conf。

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以下命令重新启动。

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]在 Linux 上, 无法在 Windows 上使用内存中 OLTP 来[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]还原数据库。 若要还原[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]使用内存中 OLTP 的数据库, 请先将数据库升级到[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]或[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] Windows 上的数据库, 然后[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]再通过备份/还原或分离/附加将它们移到 Linux 上。

- Linux 目前不支持用户权限**管理大容量操作**。

#### <a name="networking"></a>网络

如果满足以下两个条件, 则涉及 sqlservr.exe 进程的出站 TCP 连接的功能 (如链接服务器或可用性组) 可能不起作用:

1. 目标服务器指定为主机名而不是 IP 地址。

1. 源实例在内核中禁用了 IPv6。 若要验证系统中是否已启用 IPv6, 所有以下测试必须通过:

   - `cat /proc/cmdline`将打印当前内核的启动 cmdline。 输出不得包含`ipv6.disable=1`。
   - /Proc/sys/net/ipv6/目录必须存在。
   - 调用`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`应成功的 C 程序, syscall 必须返回 fd! =-1, 而不会因 EAFNOSUPPORT 而失败。

确切的错误取决于该功能。 对于链接服务器, 此清单将作为登录超时错误。 对于可用性组, 辅助`ALTER AVAILABILITY GROUP JOIN`数据库上的 DDL 将在5分钟后失败, 并出现 "下载配置超时" 错误。

若要解决此问题, 请执行以下操作之一:

1. 使用 Ip 而不是主机名来指定 TCP 连接的目标。

1. 通过从 boot cmdline 删除`ipv6.disable=1`来启用内核中的 IPv6。 执行此操作的方式取决于 Linux 分发和引导加载, 如 grub。 如果你确实想要禁用 IPv6, 则仍可以通过`net.ipv6.conf.all.disable_ipv6 = 1` `sysctl`在配置中设置来禁用它 (例如`/etc/sysctl.conf`)。 这仍会阻止系统的网络适配器获取 IPv6 地址, 但允许 sqlservr.exe 功能工作。

#### <a name="network-file-system-nfs"></a>网络文件系统 (NFS)
如果在生产环境中使用**网络文件系统 (NFS)** 远程共享, 请注意以下支持要求:

- 使用 NFS 版本**4.2 或更高**版本。 较早版本的 NFS 不支持对现代文件系统通用的必需功能, 如 fallocate 和稀疏文件创建。
- 仅查找 NFS 装载上的 **/var/opt/mssql**目录。 其他文件 (如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]系统二进制文件) 不受支持。
- 确保 NFS 客户端在装载远程共享时使用 "nolock" 选项。

#### <a name="localization"></a>本地化

- 如果在安装过程中区域设置不是英语 (en_us), 则必须在 bash 会话/终端中使用 UTF-8 编码。 如果使用 ASCII 编码, 可能会看到类似于以下内容的错误:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果无法使用 UTF-8 编码, 请使用 MSSQL_LCID 环境变量运行安装程序以指定你的语言选项。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 运行 mssql 会议安装程序并执行的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]非英语安装时, 将在本地化文本 "配置 SQL Server ..." 后显示错误的扩展字符。 或者, 对于非基于拉丁语的安装, 句子可能完全丢失。 缺少的句子应显示以下本地化字符串:"授权 PID 已成功处理。 新版本为 [\<名称\> edition] "。 此字符串只是出于信息目的而输出, 下一[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]次累积更新将针对所有语言解决此情况。 这不会[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以任何方式影响的成功安装。 

#### <a name="full-text-search"></a>全文搜索

- 并非所有筛选器都可用于此版本, 包括 Office 文档的筛选器。 有关支持的筛选器的列表, 请参阅[在 Linux 上安装 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- 此版本中的 SUSE 不支持**mssql-server**包。 它目前在 Ubuntu 和 Red Hat Enterprise Linux (RHEL) 上受支持。

- 对于[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] linux CTP 2.1 刷新和更高版本[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , 包可以使用 linux 上的 ODBC 连接。 此功能已使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和 MySQL ODBC 驱动程序进行了测试, 但也应与遵循 ODBC 规范的任何 Unicode odbc 驱动程序一起使用。 在设计时, 可以提供用于连接到 ODBC 数据的 DSN 或连接字符串;你还可以使用 Windows 身份验证。 有关详细信息, 请参阅[博客文章在 Linux 上宣布 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 在 Linux 上运行 SSIS 包时, 此版本不支持以下功能:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]目录数据库
  - SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Scale Out
  - 适用于 SSIS 的 Azure 功能包
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

有关当前不受支持的或受限制的内置 SSIS 组件列表, 请参阅[Linux 上的 SSIS 的限制和已知问题](sql-server-linux-ssis-known-issues.md#components)。

有关 Linux 上的 SSIS 的详细信息, 请参阅以下文章:
-   [博客文章宣布了对 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

在 Linux 上连接到[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的 Windows 上存在以下限制。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和中[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的数据收集器。 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]具有 Windows 身份验证或 Windows 事件日志选项的 UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 无法修改要保留的日志文件数。

## <a name="next-steps"></a>后续步骤

若要开始操作, 请参阅以下快速入门:

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [运行和连接 - 云](quickstart-install-connect-clouds.md)

有关常见问题的解答, 请参阅[LINUX 上的 SQL SERVER 常见问题解答](sql-server-linux-faq.md)。
