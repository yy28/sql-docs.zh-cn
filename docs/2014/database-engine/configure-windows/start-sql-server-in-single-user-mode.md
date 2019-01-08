---
title: 在单用户模式下启动 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 245ae929b9a267f06b675b9380760f3db6067d1c
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640888"
---
# <a name="start-sql-server-in-single-user-mode"></a>在单用户模式下启动 SQL Server
  在某些情况下，可能必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] startup option -m **在单用户模式下启动**实例。 例如，您可能要更改服务器配置选项或恢复已破坏的 master 数据库或其他系统数据库。 这两个操作都需要在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可使计算机本地 Administrators 组的任何成员作为 sysadmin 固定服务器角色的成员连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [在系统管理员被锁定时连接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，请注意下列事项：  
  
-   只有一个用户可以连接到服务器。  
  
-   不执行 CHECKPOINT 进程。 默认情况下，启动时自动执行此进程。  
  
> [!NOTE]  
>  在单用户模式下连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之前，停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务；否则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务将使用该连接，从而使其阻塞。  
  
 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的对象资源管理器可能会失败，因为在某些操作中它需要使用多个连接。 若要在单用户模式下管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，可以执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（仅通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器连接）或者使用 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。  
  
 当你将 **-m** 选项与 **sqlcmd** 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]结合使用时，可以将连接限制为指定的客户端应用程序。 例如， **-m"sqlcmd"** 将连接限制为单个连接，并且该连接必须将自身标识为 **sqlcmd** 客户端程序。 当您正在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且未知的客户端应用程序正在占用这个唯一的可用连接时，使用此选项。 若要通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器进行连接，请使用 **-m"Microsoft SQL Server Management Studio - Query"**。  
  
> [!IMPORTANT]  
>  不要将此选项作为安全功能使用。 客户端应用程序提供客户端应用程序名称，并且提供假名称来作为连接字符串的一部分。  
  
## <a name="note-for-clustered-installations"></a>针对群集安装的说明  
 对于群集环境中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，群集资源 dll 将占用可用连接，因此阻塞与服务器的任何其他连接。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处于此状态下时，如果您尝试使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理资源处于联机状态，则在该资源配置为对组产生影响时，它可能会将 SQL 资源故障转移到其他节点。  
  
 为解决此问题，请执行以下过程：  
  
1.  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高级属性中删除 -m 启动参数。  
  
2.  使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源脱机。  
  
3.  从该组的当前所有者节点，在命令提示符下发出以下命令：  
    net start MSSQLSERVER /m。  
  
4.  从群集管理器或故障转移群集管理控制台验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源仍处于脱机状态。  
  
5.  连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]现在使用以下命令并执行必需的操作：SQLCMD-E-S\<服务器名 >。  
  
6.  一旦完成该操作后，关闭命令提示符并且通过群集管理器使 SQL 和其他资源返回联机状态。  
  
## <a name="see-also"></a>请参阅  
 [启动、停止或暂停 SQL Server 代理服务](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [用于数据库管理员的诊断连接](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)   
 [检查点 (Transact-SQL)](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [数据库引擎服务启动选项](database-engine-service-startup-options.md)  
  
  
