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
ms.custom: ''
ms.date: 07/26/2019
ms.openlocfilehash: cb379078fe5d8c2436b220871d84d352a8619155
ms.sourcegitcommit: 2604e13627fbc9f3bda3926b67045fceb7b04e37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68823120"
---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) 是一种集成环境，用于管理从 SQL Server 到 Azure SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL Server 和数据库实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SSMS 在本地计算机或云端查询、设计和管理数据库及数据仓库，无论它们位于何处。

SSMS 是免费的！

## <a name="download-ssms-182"></a>下载 SSMS 18.2

SSMS 18.2 正式发布 (GA) 版本现已推出，它是为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供支持的最新一代 SQL Server Management Studio  ！

**[![下载](../ssdt/media/download.png) 下载 SQL Server Management Studio 18.2](https://go.microsoft.com/fwlink/?linkid=2099720)**

SSMS 18.2 是 SSMS 的最新正式发布 (GA) 版本。 如果安装了 SSMS 18 的上一代 GA 版本，请安装 SSMS 18.2 将其升级到 18.2。 如果安装了较早的 SSMS 18.x 预览版，请在安装 SSMS 18.2 之前将其卸载  。

**版本信息**

- 版本号：18.2  
- 生成号：15.0.18142.0  
- 发布日期：2019 年 7 月 25 日  

如果你有任何意见或建议，或想报告问题，最好是通过 [UserVoice](https://aka.ms/sqlfeedback) 与 SSMS 团队联系。

SSMS 18.x 安装不会升级或替换 SSMS 17.x 或更早版本。 SSMS 18.x 与以前的版本并行安装，因此，这两个版本均可供使用。

如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 18 

## <a name="available-languages-ssms-182"></a>可用语言 (SSMS 18.2)

此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 18.2：  
[中文（中国）](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 模块可通过 PowerShell 库单独安装。 有关详细信息，请参阅[下载 SQL Server PowerShell 模块](download-sql-server-ps-module.md)。

## <a name="new-in-this-release-ssms-182"></a>此版本 (SSMS 18.2) 中的新增功能

|  新项  |  详细信息  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 始终加密 | 更新了 Enclave Provider 以支持 Azure 证明。 |
| Intellisense/编辑器 | 添加了对数据分类的支持  |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | SSMS 索引对话框 - 添加了新索引选项 OPTIMIZE_FOR_SEQUENTIAL_KEY |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | 添加了 IntelliSense 支持 |
| 查询执行或结果 | 在消息中添加了一个“完成时间”，以跟踪给定查询执行完毕的时间。 |
| 查询执行或结果  | 允许显示更多数据（结果转换为文本）以及将其存储在单元中（结果转换为网格）。 对于这两种情况，SSMS 当前最多支持 2 百万个字符（之前分别为 25.6 万和 6.4 万）。 这还解决了用户无法从网格单元中获取超过 43680 个字符的问题。 |
| 显示计划 | 在启用了内联标量 UDF 特性 (ContainsInlineScalarTsqlUdfs) 的情况下，在 QueryPlan 中添加了新的属性。 |
| SMO | 添加了对“功能限制”*的支持。 有关功能本身的信息，请参阅[功能限制](https://docs.microsoft.com/sql/relational-databases/security/feature-restrictions)。 有关评估扩展的信息，请参阅 [SQL 评估 API 简介](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-SQL-Assessment-API-Public-Preview/ba-p/778570)。 |
| Integration Services (SSIS) | Azure 中 SSIS 包计划程序的性能优化 |
|  |  |

有关此版本中新增功能的详细信息，请参阅 [SSMS 发行说明](release-notes-ssms.md)。

## <a name="supported-sql-offerings-ssms-182"></a>受支持的 SQL 产品/服务 (SSMS 18.2)

* 此版本的 SSMS 适用于所有[受支持 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
* 此外，SSMS 18.x 可与 SSMS 17.x、SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。
* SQL Server Integration Services (SSIS) - SSMS 版本 17.x 或更高版本不支持连接到旧版 SQL Server Integration Services 服务。 要连接到早期版本的 Integration Services，请使用与 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 连接到旧版 SQL Server 2016 Integration Services 服务。 可以在同一台计算机上并行安装 SSMS 17.x 和 SSMS 16.x。 由于 SQL Server 2012 的发布，建议使用 SSIS 目录数据库 (SSISDB) 来存储、管理、运行和监视 Integration Services 包。 有关详细信息，请参阅 [SSIS 目录](../integration-services/catalog/ssis-catalog.md)。

## <a name="supported-operating-systems-ssms-182"></a>受支持的操作系统 (SSMS 18.2)

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

## <a name="release-notes-ssms-182"></a>发行说明 (SSMS 18.2)

此版本存在一些[已知问题](release-notes-ssms.md#known-issues-181)。

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
