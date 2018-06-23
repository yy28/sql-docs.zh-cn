---
title: Linux 上的 SQL Server 概述 |Microsoft Docs
description: 本主题介绍了 SQL Server 如何在 Linux 上运行和提供有关如何若要了解详细信息。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 16ea8b69f1d55e5b338931f0531bdf8a2e037707
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311685"
---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 2017 现在可以在 Linux 上运行。 它使用相同的 SQL Server 数据库引擎，具有许多相似的功能和服务，且不受操作系统的影响。

## <a name="install"></a>Install

若要开始，请使用以下快速入门教程之一在 Linux 上安装 SQL Server：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker 本身可运行在多个平台上，这意味着，你可以在 Linux、 Mac 和 Windows 上运行 Docker 映像。

## <a name="connect"></a>“连接”

安装完成后，连接到你的 Linux 计算机上的 SQL Server 实例。 你可以利用多种工具和驱动程序在本地或远程进行连接。 快速入门教程演示了如何使用 [sqlcmd](sql-server-linux-setup-tools.md) 命令行工具。 其他工具包括：

| 工具 | 教程 |
|-----|-----|
| Visual Studio Code (VS Code) | [通过 VS Code 使用 Linux 上的 SQL Server](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [在 Windows 上使用 SSMS 连接 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [通过 SSDT 使用 Linux 上的 SQL Server](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>浏览

SQL Server 2017 在所有支持的平台（包括 Linux）上具有相同的底层数据库引擎。 因此，在 Linux 上，许多现有功能的运行方式相同。 该部分的文档包含了从 Linux 角度展示的一些功能。 同时还介绍了 Linux 上的一些独特需求。

如果你已熟悉 SQL Server，请查看 [发行说明](sql-server-linux-release-notes.md) 了解常规使用说明和此版本的已知问题。 然后查看 [Linux 上的 SQL Server 的新功能](sql-server-linux-whats-new.md) 以及 [SQL Server 2017 更新概览](../sql-server/what-s-new-in-sql-server-2017.md)。 

> [!TIP]
> 有关的常见问题的答案，请参阅[Linux 常见问题的 SQL Server](sql-server-linux-faq.md)。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]