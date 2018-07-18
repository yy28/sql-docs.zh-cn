---
title: 管理 Linux 上的 SQL Server |Microsoft Docs
description: 本文提供适用于 SQL Server Linux 上运行的常见管理任务和工具的链接。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.openlocfilehash: 89b670f6b4dd815744f505d1aa4f60a29d25bcaa
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984142"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>选择合适的工具管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

有几种方法来管理 Linux 上的 SQL Server 2017。 以下部分提供了不同的管理工具和方法，并指向更多资源的快速概述。

## <a name="mssql-conf"></a>mssql-conf 
**Mssql conf**工具配置 Linux 上的 SQL Server。 有关详细信息，请参阅[在 Linux 上使用 mssql conf 配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

几乎所有在客户端工具中可以完成的工作，都可以使用 Transact - SQL 语句来完成。 SQL Server 提供了[动态管理视图 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)的查询的状态和配置 SQL Server。 此外，还有[Transact-SQL 命令](https://msdn.microsoft.com/library/bb510741.aspx)数据库管理任务。 可以在支持连接到 SQL Server 和运行 TRANSACT-SQL 查询，例如任何客户端工具中运行这些命令[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

## <a name="sql-server-operations-studio-preview"></a>SQL Server Operations Studio （预览版）

新的 Microsoft SQL Operations Studio (preview) 是用于管理 SQL Server 的跨平台工具。 有关详细信息，请参阅[Microsoft SQL Operations Studio （预览版）](../sql-operations-studio/what-is.md)。

## <a name="sql-server-management-studio-on-windows"></a>Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是一款 Windows 应用程序，它提供了一种用于管理 SQL Server 的图形用户界面。 尽管当前它只能在 Windows 上运行，但用户可以通过该应用程序远程连接到 Linux SQL Server 实例。 使用 SSMS 管理 SQL Server 的详细信息，请参阅[使用 SSMS 管理 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md)。

## <a name="mssql-cli-preview"></a>mssql cli （预览版）

Microsoft SQL Server 的发布了一个新的跨平台脚本编写工具[mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。 此工具当前处于预览状态。

## <a name="powershell"></a>PowerShell

PowerShell 提供了丰富的命令行环境，用于管理 Linux 上的 SQL Server。 有关详细信息，请参阅[使用 PowerShell 管理 Linux 上的 SQL Server](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>后续步骤

Linux 上 SQL Server 的详细信息，请参阅[Linux 上的 SQL Server](sql-server-linux-overview.md)。
