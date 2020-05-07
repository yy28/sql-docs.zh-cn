---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: b885504d8431be2df9ab0c841b47fe0eb7019932
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728634"
---
# <a name="mssqlserver_17207"></a>MSSQLSERVER_17207
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17207|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBLKIO_OS2DISKERROR|  
|消息正文|%ls:创建或打开文件 '%ls' 时出现操作系统错误 %ls。 请诊断并更正该操作系统错误，然后重试操作。|  


## <a name="explanation"></a>说明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 由于指定的 OS 错误而无法打开指定的文件。  

当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法打开数据库和/或事务日志文件时，Windows 应用程序事件或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中可能会出现错误 17207。 此错误如以下示例所示：

``` 
Error: 17207, Severity: 16, State: 1.
FileMgr::StartSecondaryDataFiles: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'F:\MSSQL\DATA\MyDB_FG1_1.ndf'. Diagnose and correct the operating system error, and retry the operation.
```

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启动过程中，或在尝试启动数据库的任何数据库操作（如 ALTER DATABASE）期间，都可能看到这些错误。 在某些情况下，你可能会看到 17207 和 17204 错误，而在其他情况下，你可能只会看到其中一种错误。

如果用户数据库遇到这些错误，该数据库将处于 RECOVERY_PENDING 状态，并且应用程序无法访问数据库。 如果系统数据库遇到这些错误，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将不会启动，并且你无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的此实例。 这也可能导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集资源脱机。

如果问题与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文件流文件组相关，你将注意到仅列出了完整目录路径，而不是文件名。 下面显示了一个示例： 
```
Error: 17207, Severity: 16, State: 1.
STREAMFCB::Startup: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\bpa_files_test_fs_1\bpa_files_test_fs_1'. Diagnose and correct the operating system error, and retry the operation.
```

## <a name="cause"></a>原因
在使用任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库之前，必须启动数据库。 数据库启动过程涉及初始化各种数据结构（这些结构表示数据库和数据库文件），打开属于数据库的所有文件，最后在数据库上运行恢复。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) Windows API 函数打开属于数据库的文件。
 
消息 17207（和 17204）指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试在启动过程中打开数据库文件时遇到错误。
 
这些错误消息包含下列信息：
1. 尝试打开文件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函数的名称。 通常在这些错误消息中看到如下函数名称：
   - FCB::Open                              - 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试打开文件时遇到错误
   - FileMgr::StartPrimaryDataFiles         - 主数据文件或属于主文件组的文件
   - FileMgr::StartSecondaryDataFiles       - 属于辅助文件组的文件
   - FileMgr::StartLogFiles                 - 事务日志文件
   - STREAMFCB::Startup                     - SQL FileStream 容器
   - FCB::RemoveAlternateStreams
  
      
1. 状态信息，用于区分可生成此错误消息的函数中的多个位置
1. 文件的完整物理路径
1. 对应于文件的文件 ID
1. 操作系统错误代码和错误说明。 在某些情况下，只会看到错误代码。
 
在这些错误消息中输出的操作系统错误信息是导致错误 17204 的根本原因。 这些错误消息的常见原因是权限问题或文件路径不正确。


## <a name="user-action"></a>用户操作  
1. 要解决错误 17207，需要了解关联的操作系统错误代码并诊断该错误。 解决了操作系统错误后，可以尝试重新启动数据库（例如，使用 ALTER DATABASE SET ONLINE）或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，使受影响的数据库处于联机状态。 在某些情况下，可能无法解决操作系统错误。 如果是这样，就必须采取具体纠正措施。 本节将介绍这些操作。
1. 如果 17207 错误消息只包含错误代码，而不包含错误说明，则可以尝试在操作系统 shell 中运行以下命令来解析错误代码：net helpmsg <error code>。 如果收到的错误代码是一个 8 位数状态代码，可以参考[如何将 HRESULT 转换为 Win32 错误代码？](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133)之类的信息源解码这些状态代码，了解它们在操作系统中都代表什么错误。
1. 如果收到 ```Access is Denied``` 操作系统错误 = 5，请考虑使用以下方法：
   -  通过在 Windows 资源管理器中查看文件的属性，检查文件的权限设置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Windows 组对各种文件资源预配访问控制。 确保相应的组[名称类似于 SQLServerMSSQLUser$ComputerName$MSSQLSERVER 或 SQLServerMSSQLUser$ComputerName$InstanceName]具有对错误消息中提及的数据库文件的必要权限。 有关更多详细信息，请参阅[配置数据库引擎访问的文件系统权限](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)。 确保 Windows 组实际包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户或服务 SID。
   -  查看当前正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的用户帐户。 可以使用 Windows 任务管理器来获取此信息。 查找可执行文件“sqlservr.exe”的“用户名”值。 另外，如果你最近更改了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户，请注意，支持执行此操作的方法是使用 SQL Server 配置管理器实用工具。 有关详细信息，请参阅 [SQL Server 配置管理器](../sql-server-configuration-manager.md)。 
   -  根据在服务器启动期间打开数据库、附加数据库、还原数据库等操作类型，用于模拟和访问数据库文件的帐户可能会有所不同。 请查看[保护数据和日志文件](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN)主题，了解哪些操作为哪些帐户设置了哪些权限。 使用 Windows SysInternals [进程监视器](https://docs.microsoft.com/sysinternals/downloads/procmon)之类的工具，了解是否在 SQL Server 实例服务启动帐户[或服务 SID] 或模拟帐户的安全上下文中执行了文件访问。

      如果 SQL Server 正在模拟可执行 ALTER DATABASE 或 CREATE DATABASE 操作的登录用户凭据，你将在进程监视器工具中注意到以下信息（例如）：
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
  
1. If you are getting ```The system cannot find the file specified``` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files which encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the ```The process cannot access the file because it is being used by another process``` operating system error = 32:
   - Use a tool like [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) or [Handle](https://docs.microsoft.com/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
  
