---
title: 数据库实例文件初始化
description: 了解即时文件初始化，并了解如何在 SQL Server 数据库上启用它。
ms.custom: contperfq4
ms.date: 05/30/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: a10e6f9cff886b18b8bc344270516aaf2b5577db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756253"
---
# <a name="database-instant-file-initialization"></a>数据库实例文件初始化
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
在本文中，你将了解即时文件初始化，还将了解如何启用它以加速 SQL Server 数据库文件的增长。  

默认情况下，初始化数据和日志文件以覆盖之前删除的文件遗留在磁盘上的任何现有数据。 执行以下操作时，应首先通过零填充（用零来填充）数据和日志文件来初始化这些文件：  
  
- 创建数据库。  
- 向现有数据库添加数据或日志文件。  
- 增大现有文件的大小（包括自动增长操作）。  
- 还原数据库或文件组。  

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，通过即时文件初始化 (IFI) 可以更快执行前面提到的文件操作，因为它会回收已使用的磁盘空间，而不会用零来填充该空间。 相反，新数据写入文件时会覆盖磁盘内容。 日志文件不能立即初始化。

## <a name="enable-instant-file-initialization"></a>启用即时文件初始化

即时文件初始化功能仅在向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户授予了 SE_MANAGE_VOLUME_NAME 之后才可用。 Windows Administrator 组的成员拥有此权限，并可以通过将其他用户添加到 **执行卷维护任务** 安全策略中来为其授予此权限。  
> [!IMPORTANT]
> 某些功能使用（如[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)）可以阻止即时文件初始化。  

> [!NOTE]
> 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，可在安装期间授予服务帐户此权限。 <br><br>如果使用[命令提示符安装](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，请添加 /SQLSVCINSTANTFILEINIT 参数，或选中[安装向导](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)中“授予 SQL Server 数据库引擎服务执行卷维护任务权限”复选框。
  
要向一个帐户授予 `Perform volume maintenance tasks` 权限：  
  
1.  在将要创建数据文件的计算机上打开本地安全策略应用程序 (`secpol.msc`)。  
  
1.  在左侧窗格中，展开“本地策略” ，然后单击“用户权限指派” 。  
  
1.  在右侧窗格中，双击“执行卷维护任务”。  
  
1.  单击“添加用户或组”并添加可运行 SQL Server 服务的帐户。  
  
1.  单击“应用” ，然后关闭所有“本地安全策略”  对话框。  

1. 重启 SQL Server 服务。

1. 在启动时检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。
   
  
    **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本开始）。
    1. 如果授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME，将记录类似如下的消息：

        `Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

    1. 如果授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME，将记录类似如下的消息：

        `Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`
    > [!NOTE]
    > 可以使用 [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV 中的 instant_file_initialization_enabled 列来识别是否启用了即时文件初始化。

## <a name="security-considerations"></a>安全注意事项

建议启用即时文件初始化，因为其优势可能远大于安全风险。

使用即时文件初始化，只有将新数据写入文件时才会覆盖已删除的磁盘内容。 出于此原因，在数据文件的该特定区域写入其他数据之前，未经授权的主体可能访问已删除的内容。

当数据库文件连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之后，可以通过文件中的随机访问控制列表 (DACL) 来降低此信息泄露的风险。 此 DACL 仅允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和本地管理员访问文件。 但是，当文件分离以后，可以由不具有 SE_MANAGE_VOLUME_NAME 的用户或服务访问。

以下情况有类似的注意事项：

* 备份数据库时。 如果未使用适当的 DACL 对备份文件进行保护，则未授权的用户或服务将可以使用删除的内容。  

* 使用 IFI 增大文件时。 SQL Server 管理员可能会访问原始页面内容并查看以前删除的内容。

* 数据库文件托管在存储区域网络中。 存储区域网络也可能始终向以预先初始化的形式提供新页面，让操作系统重新初始化页面可能会产生不必要的开销。

如果担心可能会泄漏删除的内容，则应执行以下两种或其中一种操作：  
  
- 请始终确保所有分离的数据文件和备份文件都具有限制性的 DACL。  
- 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例禁用即时文件初始化。    要进行此操作，请从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户撤消 SE_MANAGE_VOLUME_NAME。
    
    > [!NOTE]
    > 禁用该功能将延长数据文件的分配时间，且只会影响在撤消用户权限后创建的文件或增加的文件部分。
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)
