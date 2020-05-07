---
title: MSSQLSERVER_5228 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: ff8fb262b643390f2914a4a5e6c42dcc887206f8
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728614"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5120|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DSK_FCB_FAILURE|  
|消息正文|表错误:无法打开物理文件 "%.*ls"。 操作系统错误 %d: "%ls"。|  
  
## <a name="explanation"></a>说明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法打开数据库文件。  消息中提供的操作系统错误指向更具体的根本失败原因。 通常，你会看到此错误与其他错误一起出现，如 [17204](mssqlserver-17204-database-engine-error.md) 或 [17207](mssqlserver-17207-database-engine-error.md)
  
## <a name="user-action"></a>用户操作  
  
  诊断并更正该操作系统错误，然后重试操作。 有多种状态可帮助 Microsoft 缩小产品中出现错误的范围。 
  
### <a name="access-is-denied"></a>拒绝访问 
如果收到 ```Access is Denied``` 操作系统错误 = 5，请考虑使用以下方法：
   -  通过在 Windows 资源管理器中查看文件的属性，检查文件的权限设置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Windows 组对各种文件资源预配访问控制。 确保相应的组[名称类似于 SQLServerMSSQLUser$ComputerName$MSSQLSERVER 或 SQLServerMSSQLUser$ComputerName$InstanceName]具有对错误消息中提及的数据库文件的必要权限。 有关更多详细信息，请参阅[配置数据库引擎访问的文件系统权限](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)。 确保 Windows 组实际包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户或服务 SID。
   -  查看当前正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的用户帐户。 可以使用 Windows 任务管理器来获取此信息。 查找可执行文件“sqlservr.exe”的“用户名”值。 另外，如果你最近更改了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户，请注意，支持执行此操作的方法是使用 [SQL Server 配置管理器](../sql-server-configuration-manager.md)实用工具。 
   -  根据在服务器启动期间打开数据库、附加数据库、还原数据库等操作类型，用于模拟和访问数据库文件的帐户可能会有所不同。 请查看[保护数据和日志文件](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN)主题，了解哪些操作为哪些帐户设置了哪些权限。 使用 Windows SysInternals [进程监视器](https://docs.microsoft.com/sysinternals/downloads/procmon)这样的工具，了解是否在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例服务启动帐户[或服务 SID] 或模拟帐户的安全上下文中执行了文件访问。

      如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在模拟可执行 ALTER DATABASE 或 CREATE DATABASE 操作的登录用户凭据，你将在进程监视器工具中注意到以下信息（例如）：
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
  
### Attaching Files that Reside on a Network-attached storage  
If you cannot re-attach a database that resides on network-attached storage, a message like this may be logged in the Application log:

```Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).```

This problem occurs because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resets the file permissions when the database is detached. When you try to reattach the database, a failure occurs because of limited share permissions.

To resolve, follow these steps:
1. Use the -T startup option to start [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use this startup option to turn on trace flag 1802 in [SQL Server Configuration Manager](../sql-server-configuration-manager.md) (see [Trace Flags](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md) for information on 1802). For more information about how to change the startup parameters, see [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)

2. Use the following command to detach the database.
```tsql
 exec sp_detach_db DatabaseName
 go 
```

3. 使用以下命令重新附加数据库。
```tsql
exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
go
```
 
