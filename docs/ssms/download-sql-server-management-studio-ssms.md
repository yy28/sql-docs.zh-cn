---
title: 下载 SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
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
manager: craigg
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: 7993cfbf21efcbb6f984a91347987e5805741904
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67033406"
---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) 是一种集成环境，用于管理从 SQL Server 到 Azure SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL Server 和数据库实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SSMS 在本地计算机或云端查询、设计和管理数据库及数据仓库，无论它们位于何处。

SSMS 是免费的！

## <a name="download-ssms-181"></a>下载 SSMS 18.1

SSMS 18.1 通用版本 (GA) 现已推出，它是为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供支持的最新一代 SQL Server Management Studio  ！

**[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)**

SSMS 18.1 是当前 SSMS 的正式发布 (GA) 版本。 如果安装了 SSMS 18.0 (GA)，请安装 SSMS 18.1 将其升级到 18.1。 如果安装了较早的 SSMS 18.0 预览版，请在安装 SSMS 18.1 之前将其卸载。 

**版本信息**

- 版本号：18.1<br>
- 生成号：15.0.18131.0<br>
- 发布日期：2019 年 6 月 11 日

如果你有意见或建议，或想报告问题，最好是通过 [UserVoice](https://aka.ms/sqlfeedback) 与 SSMS 团队取得联系。

SSMS 18.x 安装不会升级或替换 SSMS 17.x 或更早版本。 SSMS 18.x 与以前的版本并行安装，因此，这两个版本均可供使用。

如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 18 

## <a name="available-languages-ssms-181"></a>可用语言 (SSMS 18.1)

此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 18.1：<br>
[中文（中国）](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)


> [!NOTE]
> SQL Server PowerShell 模块可通过 PowerShell 库单独安装。 有关详细信息，请参阅[下载 SQL Server PowerShell 模块](download-sql-server-ps-module.md)。

## <a name="new-in-this-release-ssms-181"></a>此版本 (SSMS 18.1) 中的新增功能

- **数据库关系图** - SSMS 中添加回了数据库关系图。 有关详细信息，请参阅[数据库关系图](https://feedback.azure.com/forums/908035/suggestions/37507828)。
- **SSBDIAGNOSE.EXE** - SQL Server 诊断命令行工具已被添加回 SSMS 包。
- **Integration Services (SSIS)** - 支持 Azure 中的计划 SSIS 包，该包位于 Azure 中的 SSIS 目录或系统文件中。 启动新建计划对话框中有三个项，新计划...  右键单击 Azure 中 SSIS 目录中的 SSIS 包时显示的菜单项，“在 Azure 中安排执行 SSIS 包”菜单项，位于“工具”菜单项下的“迁移到 Migrate”菜单项，以及右键单击 Azure SQL 数据库托管实例中的 SQL Server 代理下的作业文件夹时显示的“在 Azure 中安排执行 SSIS”    。

有关此版本中新增功能的详细信息，请参阅 [SSMS 发行说明](release-notes-ssms.md)。


## <a name="supported-sql-offerings-ssms-181"></a>受支持的 SQL 产品/服务 (SSMS 18.1)

* 此版本的 SSMS 适用于所有[受支持 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
* 此外，SSMS 18.x 可与 SSMS 17.x、SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。
* SQL Server Integration Services (SSIS) - SSMS 版本 17.x 或更高版本不支持连接到旧版 SQL Server Integration Services 服务。 要连接到早期版本的 Integration Services，请使用与 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 连接到旧版 SQL Server 2016 Integration Services 服务。 可以在同一台计算机上并行安装 SSMS 17.x 和 SSMS 16.x。 由于 SQL Server 2012 的发布，建议使用 SSIS 目录数据库 (SSISDB) 来存储、管理、运行和监视 Integration Services 包。 有关详细信息，请参阅 [SSIS 目录](../integration-services/catalog/ssis-catalog.md)。

## <a name="supported-operating-systems-ssms-181"></a>受支持的操作系统 (SSMS 18.1)

与最新可用的服务包一起使用时，此版本的 SSMS 支持以下 64 位平台：

- Windows 10（64 位）<sup>*</sup>
- Windows 8.1（64 位）
- Windows Server 2016 <sup>*</sup>
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

<sup>*</sup> 需要 1607 (10.0.14393) 或更高版本

> [!NOTE]
> SSMS 仅在 Windows 上运行。 如果需要在 Windows 以外的平台上运行的工具，请查看 Azure Data Studio。 Azure Data Studio 是一个全新的跨平台工具，可在 macOS、Linux 以及 Windows 上运行。 有关详细信息，请参阅 [Azure Data Studio](../azure-data-studio/what-is.md)。

## <a name="release-notes-ssms-181"></a>发行说明 (SSMS 18.1)

此版本没有已知问题。

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
