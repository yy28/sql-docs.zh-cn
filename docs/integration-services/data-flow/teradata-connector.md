---
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755853"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Microsoft Connector for Teradata（预览）
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

使用 Microsoft Connector for Teradata，可以从 SSIS 包内的 Teradata 数据源中导出数据以及向其中加载数据。

此新连接器支持包含 1 MB 表的数据库。

## <a name="version-support"></a>版本支持

Microsoft Connector for Teradata 支持以下 Microsoft SQL Server 产品：

- Microsoft SQL Server 2019
- Microsoft SQL Server Data Tools (SSDT)

Microsoft connector for Teradata 使用 Teradata Parallel Transporter 应用程序编程语言接口将数据加载到 Teradata 数据库中以及导出其中的数据。 支持以下版本：

- Teradata Parallel Transporter (Teradata PT) 16.10
- Teradata Parallel Transporter (Teradata PT) 16.20

支持以下 Teradata 数据库版本的数据源：

- Teradata 数据库 16.20
- Teradata 数据库 16.10
- Teradata 数据库 15.10
- Teradata 数据库 15.00

有关 Teradata Parallel Transporter 应用程序编程接口程序员指南的详细信息，请查看 [Teradata 文档](https://docs.teradata.com/)。

## <a name="installation"></a>安装

### <a name="prerequisite"></a>先决条件

在 32 位计算机上，从 [Teradata 工具和实用程序 - Windows 安装程序包](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)中安装以下驱动程序：

- Teradata ODBC 驱动程序（32 位）
- Teradata PT API（32 位）

在 64 位计算机上，安装以下驱动程序：

- Teradata ODBC 驱动程序（64 位）
- Teradata PT API（64 位）

要为 Teradata 数据库安装连接器，请从 [最新版 Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599) 下载并运行该安装程序。 然后按照安装向导中的说明进行操作。

安装连接器后，必须重启 SQL Server Integration Services，才能确保 Teradata 源和目标正常运行。

要执行面向 SQL Server 2017 及更低版本的 SSIS 包，需要安装 Microsoft Connector for Oracle by Attunity，相应版本见以下链接  ：

- [SQL Server 2017：Microsoft Connector for Teradata by Attunity 版本 5.0](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016：Microsoft Connector for Teradata by Attunity 版本 4.0](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014：Microsoft Connector for Teradata by Attunity 版本 3.0](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012：Microsoft Connector for Teradata by Attunity 版本 2.0](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>卸载

可以运行卸载向导以删除 Microsoft Connector for Teradata  。

## <a name="next-steps"></a>后续步骤

- 配置 [Teradata 连接管理器](teradata-connection-manager.md)
- 配置 [Teradata 源](teradata-source.md)
- 配置 [Teradata 目标](teradata-destination.md)
- 如有任何疑问，请访问[技术社区](https://aka.ms/AA6iwdw)。
