---
title: "在 Linux 上的 SQL Server 概述 |Microsoft 文档"
description: "本主题介绍 SQL Server 如何在 Linux 上运行和提供有关如何若要了解详细信息。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 48e2d1ae54100f7ea83bdd677bf4a98859825b67
ms.contentlocale: zh-cn
ms.lasthandoff: 10/05/2017

---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

SQL Server 2017 现在在 Linux 上运行。 它属于相同的 SQL Server 数据库引擎，具有许多相似的功能和服务，且不受操作系统的影响。

## <a name="install"></a>Install

若要开始，请在使用以下快速入门教程之一的 Linux 上安装 SQL Server:

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> 在运行 docker 本身在多个平台上，这意味着，你可以在 Linux、 Mac 和 Windows 上运行的 Docker 映像。

## <a name="connect"></a>连接

安装完成后，连接到你的 Linux 计算机上的 SQL Server 实例。 你可以连接本地或远程和各种工具和驱动程序。 快速入门教程演示如何使用[sqlcmd](sql-server-linux-setup-tools.md)命令行工具。 其他工具包括：

| 工具 | 教程 |
|-----|-----|
| Visual Studio Code (VS Code) | [将用于在 Linux 上的 SQL Server 的 VS Code](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Windows 上使用 SSMS 连接到 Linux 上的 SQL Server](sql-server-linux-develop-use-ssms.md) |
| SQL Server Data Tools (SSDT) | [结合使用 SSDT 与在 Linux 上的 SQL Server](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>浏览

SQL Server 2017 在所有支持的平台（包括 Linux）上具有相同的基础数据库引擎。 因此，在 Linux 上，许多现有功能运行方式相同。 文档的此区域显示的一些从 Linux 角度来看这些功能。 它还调用出有独特的需求在 Linux 的区域。

如果你已熟悉 SQL Server，请查看[发行说明](sql-server-linux-release-notes.md)有关的一般指导方针和对于此版本的已知的问题。 然后查看[什么是用于在 Linux 上的 SQL Server 的新功能](sql-server-linux-whats-new.md)以及[的 SQL Server 2017 总体最近更新](../sql-server/what-s-new-in-sql-server-2017.md)。

##  <a name="infotipmediageneralinfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](./media/general/info_tip.png) 与 SQL Server 工程团队合作

- [DBA 堆栈 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)： 提问数据库管理
- [堆栈溢出](http://stackoverflow.com/questions/tagged/sql-server)： 提出开发问题
- [MSDN 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)： 询问技术问题
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)： 报告 bug 和请求功能
- [Reddit](https://www.reddit.com/r/SQLServer/)： 讨论 SQL Server

