---
title: 下载 SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein, maghan
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
author: dnethi
ms.author: dinethi
ms.custom: ''
ms.date: 10/03/2019
ms.openlocfilehash: b3fa70eb83ddd46c0901cfe5d5499a0a12f33db8
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251392"
---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) 是一种集成环境，用于管理从 SQL Server 到 Azure SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL Server 和数据库实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SSMS 在本地计算机或云端查询、设计和管理数据库及数据仓库，无论它们位于何处。

SSMS 是免费的！

## <a name="download-ssms-1831"></a>下载 SSMS 18.3.1

**SSMS 18.3.1 现已推出，它是为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供支持的 *SQL Server Management Studio* 的最新通用版 (GA)！**

**[下载 SQL Server Management Studio 18.3.1](https://go.microsoft.com/fwlink/?linkid=2105412)**

SSMS 18.3.1 是 SSMS 的最新通用版 (GA)。 如果安装了以前的 SSMS 18 通用版，则安装 SSMS 18.3.1 会将其升级到 18.3.1。如果安装的是旧版 SSMS 18.x 预览版，则必须先将其卸载，然后再安装 SSMS 18.3.1。

**版本信息**

- 版本号：18.3.1  
- 生成号：15.0.18183.0  
- 发布日期：2019 年 10 月 2 日  

如果你有任何意见或建议，或想报告问题，最好是通过 [UserVoice](https://aka.ms/sqlfeedback) 与 SSMS 团队联系。

SSMS 18.x 安装不会升级或替换 SSMS 17.x 或更早版本。 SSMS 18.x 与以前的版本并行安装，因此，这两个版本均可供使用。

如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 18

## <a name="available-languages-ssms-1831"></a>可用语言 (SSMS 18.3.1)

此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 18.3.1：  
[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 模块可通过 PowerShell 库单独安装。 有关详细信息，请参阅[下载 SQL Server PowerShell 模块](download-sql-server-ps-module.md)。

## <a name="new-in-this-release-ssms-1831"></a>此版本 (SSMS 18.3.1) 中的新增功能

| 新建项 | 详细信息 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数据分类 | 向列属性 UI 添加数据分类信息（信息类型、信息类型 ID、敏感度标签和敏感度标签 ID 未在 SSMS UI 中公开）。 |
| Intellisense/编辑器 | 更新了对最近添加到 SQL Server 2019 中的功能的支持（例如，“ALTER SERVER CONFIGURATION”）。 |
| Integration Services | 添加新的选择菜单项 `Tools > Migrate to Azure > Configure Azure-enabled DTExec`，该菜单项将 Azure-SSIS Integration Runtime 上的 SSIS 包执行作为 ADF 管道中的“执行 SSIS 包”活动调用。 |
| SMO/脚本 | 添加了对 Azure SQL DW 唯一约束的支持脚本的支持。 |
| SMO/脚本 | 数据分类 - 添加了对 SQL 版本 10 (SQL 2008) 及更高版本的支持。  - 为 SQL 版本 15 (SQL 2019) 和更高版本以及 Azure SQL DB 添加了新的敏感度属性“rank”。 |

有关此版本中新增功能的详细信息，请参阅 [SSMS 发行说明](release-notes-ssms.md)。

## <a name="supported-sql-offerings-ssms-1831"></a>受支持的 SQL 产品/服务 (SSMS 18.3.1)

- 此版本的 SSMS 适用于所有[受支持 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
- 此外，SSMS 18.x 可与 SSMS 17.x、SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。
- SQL Server Integration Services (SSIS) - SSMS 版本 17.x 或更高版本不支持连接到旧版 SQL Server Integration Services 服务。 要连接到早期版本的 Integration Services，请使用与 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 连接到旧版 SQL Server 2016 Integration Services 服务。 可以在同一台计算机上并行安装 SSMS 17.x 和 SSMS 16.x。 由于 SQL Server 2012 的发布，建议使用 SSIS 目录数据库 (SSISDB) 来存储、管理、运行和监视 Integration Services 包。 有关详细信息，请参阅 [SSIS 目录](../integration-services/catalog/ssis-catalog.md)。

## <a name="supported-operating-systems-ssms-1831"></a>受支持的操作系统 (SSMS 18.3.1)

与最新可用的服务包一起使用时，此版本的 SSMS 支持以下 64 位平台：

- Windows 10（64 位）<sup>*</sup>
- Windows 8.1（64 位）
- Windows Server 2019（64 位）
- Windows Server 2016（64 位）<sup>*</sup>
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

<sup>*</sup> 需要 1607 (10.0.14393) 或更高版本

> [!NOTE]
> SSMS 仅在 Windows 上运行。 如果需要在 Windows 以外的平台上运行的工具，请查看 Azure Data Studio。 Azure Data Studio 是一个全新的跨平台工具，可在 macOS、Linux 以及 Windows 上运行。 有关详细信息，请参阅 [Azure Data Studio](../azure-data-studio/what-is.md)。

## <a name="release-notes-ssms-1831"></a>发行说明 (SSMS 18.3.1)

此版本存在一些[已知问题](release-notes-ssms.md#known-issues-1831)。

有关此版本的详细信息，请参阅 [SSMS 发行说明](release-notes-ssms.md)。

## <a name="previous-ssms-releases"></a>SSMS 的早期版本

[旧版 SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>另请参阅

- [教程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文档](sql-server-management-studio-ssms.md)
- [其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
