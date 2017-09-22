---
title: "管理在 Linux 上的 SQL Server |Microsoft 文档"
description: "本主题提供有关 SQL Server 运行在 Linux 上的常见管理任务和工具的链接。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 5f7c0f61cf9f441c56529ddaaddc96a0c318ce59
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>选择合适的工具管理 Linux 上的 SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

有多种方法来管理在 Linux 上的 SQL Server 自 2017 年 1 RC2。 以下部分提供不同的管理工具和技术使用指向更多资源的快速概述。

## <a name="mssql-conf"></a>mssql conf 
**Mssql conf**工具在 Linux 上配置 SQL Server。 有关详细信息，请参阅[mssql conf 与 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

几乎所有在客户端工具中可以完成的工作，都可以使用 Transact - SQL 语句来完成。 SQL Server 提供[动态管理视图 (Dmv)](/sql-docs/docs/relational-databases/system-dynamic-management-views/system-dynamic-management-views) ，查询的状态和配置 SQL Server。 也有[TRANSACT-SQL 命令](https://msdn.microsoft.com/library/bb510741.aspx)数据库管理任务。 可以在任何支持连接到 SQL Server 并运行 Transact - SQL 查询的客户端工具中运行这些命令。 示例包括[sqlcmd](sql-server-linux-setup-tools.md)， [Visual Studio Code](sql-server-linux-develop-use-vscode.md)，和[SQL Server Management Studio](sql-server-linux-manage-ssms.md)。

## <a name="sql-server-management-studio-on-windows"></a>Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是一款 Windows 应用程序，它提供了一种用于管理 SQL Server 的图形用户界面。 尽管当前它只能在 Windows 上运行，但用户可以通过该应用程序远程连接到 Linux SQL Server 实例。 有关使用 SSMS 管理 SQL Server 的详细信息，请参阅[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

## <a name="powershell"></a>PowerShell

PowerShell 提供了丰富的命令行环境，用于管理 Linux 上的 SQL Server。 有关详细信息，请参阅[管理 Linux 上的 SQL server 使用 PowerShell](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>后续步骤

在 Linux 上 SQL Server 的详细信息，请参阅[在 Linux 上的 SQL Server](sql-server-linux-overview.md)。
