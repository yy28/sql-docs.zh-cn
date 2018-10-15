---
title: 下载 SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dda660429182ad7627ec65afda84ccd0765e81c1
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851772"
---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
SSMS 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL 实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SQL Server Management Studio (SSMS) 在本地计算机或云端查询、设计和管理数据库和数据仓库，无论它们位于何处。

**SSMS 是免费的！**

SSMS 18.0（预览版 4）是最新一代的 SQL Server Management Studio，可支持 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]。

[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 18.0（预览版 4）](https://go.microsoft.com/fwlink/?linkid=2014662)

预览版 4 是 SSMS 18.0 的首个公共预览版。 有关 SSMS 的最新正式发布 (GA) 版本，请[下载并安装 SSMS 17.9](sql-server-management-studio-changelog-ssms.md#ssms-179-latest-ga-release)。

**版本信息**

版本号：18.0（预览版 4）<br>
生成号：15.0.18040.0<br>
发布日期：2018 年 9 月 24 日

预览版 4 是 SSMS 18.0 的首个公共预览版。

如果你有意见或建议，或想报告问题，最好是通过 [UserVoice](https://aka.ms/sqlfeedback) 与 SSMS 团队取得联系。 SSMS 18.0 是预览版产品。 请勿在此页底部添加注释！

SSMS 18.x 安装不会升级或替换 SSMS 17.x 或更早版本。 SSMS 18.x 与以前的版本并行安装，因此，这两个版本均可供使用。

如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 18：
 

## <a name="available-languages"></a>可用语言

此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 18.0（预览版 4）：<br>
[中文（中国）](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2014662&clcid=0x40a)

SQL Server Management Studio 18.0 升级包（升级到 18.0）：<br>
此时没有可用的升级选项。

> [!NOTE]
> SQL Server PowerShell 模块可通过 PowerShell 库单独安装。 有关详细信息，请参阅[下载 SQL Server PowerShell 模块](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio


## <a name="new-in-this-release"></a>此版本中的新增功能

SSMS 18.0（预览版）是最新版 SQL Server Management Studio。 SSMS 的 18.x 一代提供对 SQL Server 2008 到 SQL Server 2019 预览版几乎所有功能领域的支持。

有关此版本中新增功能的详细信息，请参阅 [SSMS 更改日志](sql-server-management-studio-changelog-ssms.md)。


## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

* 此版本的 SSMS 适用于所有[受支持 SQL Server 2008 - [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
* 此外，SSMS 18.x 可与 SSMS 17.x、SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。
* SQL Server Integration Services (SSIS) - SSMS 版本 17.x 或更高版本不支持连接到旧版 SQL Server Integration Services 服务。 要连接到早期版本的 Integration Services，请使用与 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 连接到旧版 SQL Server 2016 Integration Services 服务。 可以在同一台计算机上并行安装 SSMS 17.x 和 SSMS 16.x。 由于 SQL Server 2012 的发布，建议使用 SSIS 目录数据库 (SSISDB) 来存储、管理、运行和监视 Integration Services 包。 有关详细信息，请参阅 [SSIS 目录](../integration-services/catalog/ssis-catalog.md)。

## <a name="supported-operating-systems"></a>受支持的操作系统

与最新可用的服务包一起使用时，此版本的 SSMS 支持以下 64 位平台：

- Windows 10（64 位） *
- Windows Server 2016 *
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

\* 需要版本 1607 (10.0.14939) 或更高版本

> [!NOTE]
> SSMS 仅在 Windows 上运行。 如果需要在 Windows 以外的平台上运行的工具，请查看 Azure Data Studio。 Azure Data Studio 是一个全新的跨平台工具，可在 macOS、Linux 以及 Windows 上运行。 有关详细信息，请参阅 [Azure Data Studio](../azure-data-studio/what-is.md)。
  
## <a name="ssms-installation-tips-and-issues"></a>SSMS 安装提示和问题

### <a name="minimize-installation-reboots"></a>尽量减少安装重启的次数

* 执行以下操作以降低 SSMS 安装程序在安装结束时需要重新启动的可能性：
  * 请确保运行的是最新版 Visual C++ 2013 Redistributable Package。 需要版本 12.0.40649.5（或更高版本）。 仅需要版本 x64。
  * 验证计算机上的 .NET Framework 版本是否为 4.6.1（或更高版本）。
  * 关闭计算机上打开的其他任何 Visual Studio 实例。
  * 请确保计算机上已安装所有最新 OS 更新。
  * 所提及的操作通常只需执行一次。 有几种情况需要在额外升级到 SSMS 的同一主版本期间重新启动。 对于次要升级，计算机上已安装 SSMS 的所有要求。


## <a name="release-notes"></a>发行说明

以下是当前版本中的已知问题：

> [!IMPORTANT]
> 使用带有 SQL 查询编辑器的“Active Directory - 通用且具有 MFA 支持”身份验证时，用户可能会遇到关闭连接并在每次查询调用时重新打开连接的问题。 此类闭包的副作用包括意外删除全局临时表，有时会向连接提供新的 SPID。 如果连接上存在打开的事务，则不会发生闭包。 若要解决此问题，用户可以在连接参数中设置 `persist security info=true`。

SSMS

- 双击 .sql 文件将启动 SSMS，但不会打开实际脚本。
  - 解决方法：将 .sql 文件拖放到 SSMS 编辑器上。

SSIS

- 当面向旧版本的 SQL Server 并且同时包含脚本任务/脚本组件时，无法成功部署或执行包。
- SSMS 无法连接到远程 Integration Services。


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


如果你有意见或建议，或想报告问题，最好是通过 [UserVoice](https://aka.ms/sqlfeedback) 与 SSMS 团队取得联系。
