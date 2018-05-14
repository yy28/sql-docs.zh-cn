---
title: 下载 SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- 安装 SSMS，下载 SSMS，最新的 SSMS
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- SQL Management Studio 安装
- 下载 SQL Management Studio
- MS SQL Management Studio
- 安装 SQL Management Studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8a10829deda74850da86bfb066ad95a6effac83
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
SSMS 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL 实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SQL Server Management Studio (SSMS) 在本地计算机或云端查询、设计和管理数据库和数据仓库，无论它们位于何处。

**SSMS 是免费的！**

SSMS 17.x 是最新一代的 SQL Server Management Studio，可支持 SQL Server 2017。

[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 17.6](https://go.microsoft.com/fwlink/?linkid=870039)

[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 17.6 升级包（将 17.x 升级到 17.6）](https://go.microsoft.com/fwlink/?linkid=870041)

> [!WARNING]
> 存在已知问题：当使用[维护计划](../relational-databases/maintenance-plans/maintenance-plans.md)时，SSMS 17.6 变得不稳定，甚至崩溃。 如果使用维护计划，请勿安装 SSMS 17.6。 如果已经安装 SSMS 17.6，且此问题正在产生不良影响，请降级到 17.5。 

**版本信息**

版本号：17.6<br>
生成号：14.0.17230.0<br>
发布日期：2018 年 3 月 20 日

SSMS 17.x 安装不会升级或替换 SSMS 16.x 或更早版本。 SSMS 17.x 与以前的版本并行安装，因此，这两个版本均可供使用。
如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 17，并有一个新图标： 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


## <a name="available-languages"></a>可用语言

> [!NOTE]
> 如果安装在以下平台中，非英语本地化版本的 SSMS 需要 [KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966)：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。


此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 17.6：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40a)

SQL Server Management Studio 17.6 升级包（将 17.x 升级到 17.6）：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=870041&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 模块现可通过 PowerShell 库单独安装。 有关详细信息，请参阅[下载 SQL Server PowerShell 模块](download-sql-server-ps-module.md)。
## <a name="sql-server-management-studio"></a>SQL Server Management Studio


## <a name="new-in-this-release"></a>此版本中的新增功能

SSMS 17.6 是 SQL Server Management Studio 的最新版本。 SSMS 的 17.x 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。 版本 17.x 也支持 SQL Analysis Service PaaS。

版本 17.6 包括：

**常规 SSMS**

SQL 数据库托管实例：

- 添加了对 [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)的支持。 Azure SQL 数据库托管实例（预览版）是 Azure SQL 数据库的一种新风格，提供与本地 SQL Server 的接近 100% 的兼容性，是一个解决常见安全问题的本机[虚拟网络 (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 实现和一个有利于本地 SQL Server 客户的[业务模型](https://azure.microsoft.com/pricing/details/sql-database/)。
- 支持常见管理方案，例如：
   - 创建和更改数据库。
   - 备份和还原数据库。
   - 导入、导出、提取和发布数据层应用程序。
   - 查看和更改服务器属性。
   - 完全支持对象资源管理器。
   - 编写数据库对象的脚本。
   - 支持 SQL 代理作业。
   - 支持链接服务器。
- 在[此处](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/)了解有关托管实例的更多信息。


对象资源管理器：
- 添加了设置，以便在从对象资源管理器拖放至查询窗口时，不强制使用括号括住名称。 （用户建议 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 和 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)。）

数据分类：
- 一般改进和 bug 修复。

**Integration Services (IS)**

- 添加了支持，便于将包部署到 [SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。

## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

* 此版本的 SSMS 适用于所有[受支持 SQL Server 版本 (SQL Server 2008 - SQL Server 2017)](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
* 使用 SSMS 17.x 连接到 [Linux 上的 SQL Server](../linux/sql-server-linux-overview.md)。
* 此外，SSMS 17.x 可与 SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。
* SQL Server Integration Services (SSIS) - SSMS 版本 17.x 不支持连接到旧版 SQL Server Integration Services 服务。 要连接到早期版本的 Integration Services，请使用与 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 连接到旧版 SQL Server 2016 Integration Services 服务。 可以在同一台计算机上并行安装 SSMS 17.x 和 SSMS 16.x。 由于 SQL Server 2012 的发布，建议使用 SSIS 目录数据库 (SSISDB) 来存储、管理、运行和监视 Integration Services 包。 有关详细信息，请参阅 [SSIS 目录](../integration-services/catalog/ssis-catalog.md)。

## <a name="supported-operating-systems"></a>受支持的操作系统
  
与最新可用的服务包一起使用时，此版本的 SSMS 支持以下 64 位平台：
- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1)（64 位）
- Windows Server 2016 *
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

\*SSMS 17.X 基于 Windows Server 2016 之前发布的 Visual Studio 2015 独立 shell。 Microsoft 非常重视应用兼容性，确保已发布的应用程序能在 Windows 最新版本上继续运行。 若要尽量减少在 Windows Server 2016 上运行 SSMS 时出现的问题，请确保 SSMS 已应用所有最新更新。 如果遇到与 Windows Server 2016 版 SSMS 有关的任何问题，请联系支持人员。 支持团队将确定问题是与 SSMS、Visual Studio 还是与 Windows 兼容性相关。 然后，支持团队将问题交接给相应的团队进行进一步调查。

## <a name="ssms-installation-tips-and-issues"></a>SSMS 安装提示和问题

### <a name="minimize-installation-reboots"></a>尽量减少安装重启的次数

* 执行以下操作以降低 SSMS 安装程序在安装结束时需要重新启动的可能性：
  * 请确保运行的是最新版 Visual C++ 2013 Redistributable Package。 需要版本 12.0.40649.5（或更高版本）。 仅需要版本 x64。
  * 验证计算机上的 .NET Framework 版本是否为 4.6.1（或更高版本）。
  * 关闭计算机上打开的其他任何 Visual Studio 实例。
  * 请确保计算机上已安装所有最新 OS 更新。
  * 所提及的操作通常只需执行一次。 有几种情况需要在额外升级到 SSMS 的同一主版本期间重新启动。 对于次要升级，计算机上已安装 SSMS 的所有要求。


## <a name="release-notes"></a>发行说明

以下是此 17.6 版本的问题和限制：

目前存在一个已知问题，即在维护计划中配置日程安排时，SSMS 17.6 会发生故障。


## <a name="previous-releases"></a>以前的版本

[旧版 SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>反馈

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>另请参阅

- [教程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文档](sql-server-management-studio-ssms.md)
- [其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]