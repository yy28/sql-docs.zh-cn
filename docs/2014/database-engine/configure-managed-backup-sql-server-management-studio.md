---
title: 配置托管的备份 (SQL Server Management Studio) |Microsoft 文档
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d3dfda6b4fb970f9ee8424cd3eec2e72bf0a22b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124843"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>配置托管备份 (SQL Server Management Studio)
  **Managed Backup**对话框允许你配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]实例的默认值。 本主题介绍如何使用此对话框可以配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]实例和执行此操作时必须考虑的选项的默认设置。 当[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]配置对于实例，这些设置应用于此后创建任何新数据库。  
  
 如果你想要配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]特定数据库，请参阅[启用和配置 SQL Server Managed Backup to Windows Azure 中针对数据库](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
 
> [!NOTE] 
> 代理服务器不支持 SQL Server 托管备份。 
  
## <a name="task-list"></a>任务列表  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 函数使用托管在 SQL Server Management Studio 备份接口  
 在此版本中，你可以仅配置实例级别默认设置，请使用**管理备份**接口。 无法配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]对于数据库，暂停或恢复[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]操作或安装电子邮件通知。 有关如何执行操作当前不支持通过**Managed Backup**接口，请参阅[SQL Server Managed Backup to Windows Azure-保持和存储设置](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
## <a name="permissions"></a>权限  
 **查看托管备份节点是 SQL Server Management Studio:** 若要查看**Managed Backup**中的节点**对象资源管理器**，你必须是系统管理员或具有以下权限指定授予给你的用户帐户：  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` 上`smart_admin.fn_is_master_switch_on`。  
  
-   `SELECT` 上`smart_admin.fn_backup_instance_config`。  
  
 **配置托管备份：** 配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在 SQL Server Management Studio，你必须是系统管理员或具有以下权限：  
  
 中的成员身份`db_backupoperator`与数据库角色，`ALTER ANY CREDENTIAL`权限，和`EXECUTE`权限`sp_delete_backuphistory`存储过程。  
  
 `SELECT` 权限`smart_admin.fn_get_current_xevent_settings`函数。  
  
 `EXECUTE` 权限`smart_admin.sp_get_backup_diagnostics`存储过程。 此外，它还需要 `VIEW SERVER STATE` 权限，因为它在内部调用其他需要此权限的系统对象。  
  
 `EXECUTE` 权限`smart_admin.sp_set_instance_backup`，和`smart_admin.sp_backup_master_switch`。  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用 SQL Server Management Studio  
 从**对象资源管理器**，展开**管理**节点，然后右键单击**Managed Backup**。 选择 **“配置”**。 这将打开 **“托管备份”** 对话框。  
  
 检查**启用托管备份**选项并指定配置值：  
  
 **文件保留**周期以天为单位指定和应介于 1 和 30 之间。  
  
 **SQL 凭据**你选择应匹配的存储帐户。 如果你当前没有一个存储身份验证信息的 SQL 凭据，则可以创建一个通过单击**创建**。 你还可以通过使用 CREATE CREDENTIAL Transact-SQL 语句创建凭据，并提供用于身份识别的存储帐户名和用于 SECRET 参数的访问密钥。 有关详细信息，请参阅[创建凭据](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential)。  
  
 指定**存储 URL**对于 Windows Azure 存储帐户，SQL 凭据存储存储帐户的身份验证信息和备份文件的保持期。  
  
 存储 URL 格式： https://\<StorageAccount >.blob.core.windows.net/  
  
 若要在实例级别设置的加密设置，请检查**加密备份**选项，并指定该算法的证书或非对称密钥用于加密。  以实例级别设置的此值将用于应用此配置后创建的所有新数据库。  
  
> [!WARNING]  
>  不能使用此对话框可以指定的加密选项，而配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 这些加密选项仅适用于[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]操作。 若要对其他备份过程进行加密，请参阅[备份加密](../relational-databases/backup-restore/backup-encryption.md)。  
  
### <a name="considerations"></a>注意事项  
 如果你配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在实例级别设置适用于此后创建任何新数据库。  然而，现有数据库将不会自动继承这些设置。 若要配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上以前存在的数据库，则必须专门配置每个数据库。 有关详细信息，请参阅[启用和配置 SQL Server Managed Backup to Windows Azure 中针对数据库](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
  
 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已使用暂停`smart_admin.sp_backup_master_switch`，你将看到一条警告消息"托管备份处于禁用状态和当前配置才会生效..." 。 使用`smart_admin.sp_backup_master_switch`存储，并且设置@new_state= 1。 这将恢复[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]服务和配置设置将生效。 存储过程的详细信息，请参阅[smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [针对 Microsoft Azure 的 SQL Server 托管备份：互操作性和共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
