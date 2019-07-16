---
title: Linux 上的 SQL Server 概述
description: 本主题介绍了 SQL Server 如何在 Linux 上运行和提供有关如何若要了解详细信息。
author: VanMSFT
ms.author: vanto
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: e3bd50cba4bcab81e7dcf00db9394704c5486160
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105457"
---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
从 SQL Server 2017 开始，SQL Server 在 Linux 上运行。 它是相同的 SQL Server 数据库引擎，与许多类似的功能和服务而不考虑您的操作系统。
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
SQL Server 2019 预览版在 Linux 上运行。 它是相同的 SQL Server 数据库引擎，与许多类似的功能和服务而不考虑您的操作系统。 若要了解有关此版本的详细信息，请参阅[什么是适用于 Linux 的 SQL Server 2019 preview 中的新增](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [SQL Server 2019 预览](sql-server-linux-overview.md?view=sql-server-ver15)已发布 ！ 若要了解什么是适用于 Linux 的最新版本中的新增功能，请参阅[什么是适用于 Linux 的 SQL Server 2019 preview 中的新增](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [SQL Server 2019 预览](sql-server-linux-overview.md?view=sql-server-linux-ver15)已发布 ！ 若要了解什么是适用于 Linux 的最新版本中的新增功能，请参阅[什么是适用于 Linux 的 SQL Server 2019 preview 中的新增](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-linux-ver15#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> SQL Server 2019 预览版已发布 ！ 若要了解什么是适用于 Linux 的最新版本中的新增功能，请参阅[什么是适用于 Linux 的 SQL Server 2019 preview 中的新增](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)。
::: moniker-end

## <a name="install"></a>安装

若要开始，请使用以下快速入门教程之一在 Linux 上安装 SQL Server：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

> [!NOTE]
> Docker 本身可运行在多个平台上，这意味着，你可以在 Linux、 Mac 和 Windows 上运行 Docker 映像。

## <a name="connect"></a>连接

安装完成后，连接到你的 Linux 计算机上的 SQL Server 实例。 你可以利用多种工具和驱动程序在本地或远程进行连接。 快速入门教程演示了如何使用 [sqlcmd](sql-server-linux-setup-tools.md) 命令行工具。 其他工具包括：

| Tool | 教程 |
|-----|-----|
| Visual Studio Code (VS Code) | [通过 VS Code 使用 Linux 上的 SQL Server](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [在 Windows 上使用 SSMS 连接 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [通过 SSDT 使用 Linux 上的 SQL Server](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>浏览

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017 在所有支持的平台（包括 Linux）上具有相同的底层数据库引擎。 因此，许多现有特性和功能运行在 Linux 上相同的方式。 该部分的文档包含了从 Linux 角度展示的一些功能。 同时还介绍了 Linux 上的一些独特需求。

如果你已熟悉 SQL Server，请查看 [发行说明](sql-server-linux-release-notes.md) 了解常规使用说明和此版本的已知问题。 然后查看 [Linux 上的 SQL Server 的新功能](sql-server-linux-whats-new.md) 以及 [SQL Server 2017 更新概览](../sql-server/what-s-new-in-sql-server-2017.md)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 所有支持的平台，包括 Linux 上具有相同的基础数据库引擎。 因此，许多现有特性和功能运行在 Linux 上相同的方式。 该部分的文档包含了从 Linux 角度展示的一些功能。 同时还介绍了 Linux 上的一些独特需求。

如果你已熟悉 Linux 上的 SQL Server，请查看[发行说明](sql-server-linux-release-notes-2019.md)的一般指导原则和此版本的已知的问题。 再看[what's new for Linux 上的 SQL Server 2019 预览](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)。

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 和[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]所有支持的平台，包括 Linux 上具有相同的基础数据库引擎。 因此，许多现有特性和功能运行在 Linux 上相同的方式。 该部分的文档包含了从 Linux 角度展示的一些功能。 同时还介绍了 Linux 上的一些独特需求。

如果你已熟悉 Linux 上的 SQL Server，请查看发行说明：

- [SQL Server 2017 发行说明](sql-server-linux-release-notes.md)
- [SQL Server 2019 预览版发行说明](sql-server-linux-release-notes-2019.md)

然后看看哪些新增功能：

- [什么是 SQL Server 2017 的新增功能](sql-server-linux-whats-new.md)
- [什么是新的 Linux 上的 SQL Server 2019 预览](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> 有关常见问题的解答，请参阅[SQL Server Linux 常见问题](sql-server-linux-faq.md)。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
