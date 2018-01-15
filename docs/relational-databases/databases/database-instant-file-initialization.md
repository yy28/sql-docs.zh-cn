---
title: "数据库实例文件初始化 | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: cf0f0006186bde39228ac9b0039e5a45b42431b7
ms.sourcegitcommit: b4b7cd787079fa3244e77c1e9e3c68723ad30ad4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="database-file-initialization"></a>数据库文件初始化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]初始化数据和日志文件以覆盖之前删除的文件遗留在磁盘上的任何现有数据。 执行以下其中一项操作时，应首先通过零填充（用零填充）数据和日志文件来初始化这些文件：  
  
- 创建数据库。  
- 向现有数据库添加数据或日志文件。  
- 增大现有文件的大小（包括自动增长操作）。  
- 还原数据库或文件组。  
  
文件初始化会导致这些操作花费更多时间。 但是，首次将数据写入文件后，操作系统就不必用零来填充文件。  
  
## <a name="instant-file-initialization-ifi"></a>即时文件初始化 (IFI)  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可以在瞬间对数据文件进行初始化，以避免零填充操作。 即时文件初始化可以快速执行上述文件操作。 即时文件初始化功能将回收使用的磁盘空间，而无需使用零填充空间。 相反，新数据写入文件时会覆盖磁盘内容。 日志文件不能立即初始化。  
  
> [!NOTE]  
> 只有在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 或 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或更高版本中才可以使用即时文件初始化功能。  

> [!IMPORTANT]
> 只有在数据文件中才可以使用即时文件初始化功能。 创建日志文件或其大小增长时，将始终零填充该文件。
  
即时文件初始化功能仅在向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户授予了 SE_MANAGE_VOLUME_NAME 之后才可用。 Windows Administrator 组的成员拥有此权限，并可以通过将其他用户添加到 **执行卷维护任务** 安全策略中来为其授予此权限。  
  
> [!IMPORTANT]
> 某些功能使用（如[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)）可以阻止即时文件初始化。  
  
要向一个帐户授予 `Perform volume maintenance tasks` 权限：  
  
1.  在将要创建备份文件的计算机上打开**本地安全策略**应用程序 (`secpol.msc`)。  
  
2.  在左侧窗格中，展开“本地策略” ，然后单击“用户权限指派” 。  
  
3.  在右侧窗格中，双击“执行卷维护任务”。  
  
4.  单击“添加用户或组”  ，添加用于备份的任何用户帐户。  
  
5.  单击“应用” ，然后关闭所有“本地安全策略”  对话框。  

> [!NOTE]
> 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，可在安装期间授予服务帐户此权限。 如果使用[命令提示符安装](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，请添加 /SQLSVCINSTANTFILEINIT 参数，或选中[安装向导](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)中“授予 SQL Server 数据库引擎服务执行卷维护任务权限”复选框。

> [!NOTE]
> 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 开始，[sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV 中的列 *instant_file_initialization_enabled* 可用来识别是否启用了即时文件初始化。

## <a name="remarks"></a>Remarks
如果授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME，则会在启动时在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中记录类似以下内容的消息： 

```
Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

如果未授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME，则不会在启动时在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中记录类似以下内容的消息： 

```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**适用于：**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 开始）

## <a name="security-considerations"></a>需要考虑的安全性因素  
使用即时文件初始化 (IFI) 时，由于只有在新数据写入文件中时才覆盖删除的磁盘内容，因此，在数据文件的该特定区域中发生某些其他的数据写入前，未授权的主体可能会访问删除的内容。 当数据库文件连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之后，可以通过文件中的随机访问控制列表 (DACL) 来降低此信息泄露的风险。 此 DACL 仅允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和本地管理员访问文件。 但是，当文件分离以后，可以由不具有 SE_MANAGE_VOLUME_NAME 的用户或服务访问。 备份数据库时，将需要以下类似考虑：如果未使用适当的 DACL 对备份文件进行保护，则未授权的用户或服务将可以使用删除的内容。  
 
> [!NOTE]
> 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装在安全物理环境中，启用即时文件初始化的性能优势在权衡时胜过带来的安全风险，这也是建议进行此操作的原因。
  
如果担心可能会泄漏删除的内容，则应执行以下两种或其中一种操作：  
  
- 请始终确保所有分离的数据文件和备份文件都具有限制性的 DACL。  
- 通过从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户中撤消 SE_MANAGE_VOLUME_NAME 来禁用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的即时文件初始化功能。 

> [!IMPORTANT]
> 禁用即时文件初始化将增加数据文件的分配时间。  
  
> [!NOTE]  
> 禁用即时文件初始化功能只会影响在用户权限撤消之后创建的文件或其大小增大的文件。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
