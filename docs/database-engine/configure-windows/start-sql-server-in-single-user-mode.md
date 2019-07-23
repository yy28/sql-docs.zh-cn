---
title: 在单用户模式下启动 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1cb488b6ce3dc21567b4f64738f9c26910c61f17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037161"
---
# <a name="start-sql-server-in-single-user-mode"></a>在单用户模式下启动 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在某些情况下，可能必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] startup option -m **在单用户模式下启动**实例。 例如，您可能要更改服务器配置选项或恢复已破坏的 master 数据库或其他系统数据库。 这两个操作都需要在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可使计算机本地 Administrators 组的任何成员作为 sysadmin 固定服务器角色的成员连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [在系统管理员被锁定时连接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，请注意下列事项：  
  
-   只有一个用户可以连接到服务器。  
  
-   不执行 CHECKPOINT 进程。 默认情况下，启动时自动执行此进程。  
  
> [!NOTE]  
>  在单用户模式下连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之前，停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务；否则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务将使用该连接，从而使其阻塞。  
  
在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的对象资源管理器可能会失败，因为在某些操作中它需要使用多个连接。 若要在单用户模式下管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，可以执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（仅通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器连接）或者使用 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。  
  
将 -m  选项与 SQLCMD  或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 结合使用时，可将连接限制为指定客户端应用程序。 

> [!NOTE]
> 在 Linux 上，SQLCMD  必须大写，如下所示。

例如，-m"sqlcmd"  将连接限制为单个连接，并且该连接必须将自身标识为 SQLCMD  客户端程序。 当您正在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且未知的客户端应用程序正在占用这个唯一的可用连接时，使用此选项。 若要通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器进行连接，请使用 **-m"Microsoft SQL Server Management Studio - Query"** 。  
  
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
  
5.  现在使用以下命令连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且执行必需的操作：SQLCMD -E -S\<servername>。  
  
6.  一旦完成该操作后，关闭命令提示符并且通过群集管理器使 SQL 和其他资源返回联机状态。  
  
## <a name="see-also"></a>另请参阅  
 [启动、停止或暂停 SQL Server 代理服务](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [用于数据库管理员的诊断连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)   
 [检查点 (Transact-SQL)](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [数据库引擎服务启动选项](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
