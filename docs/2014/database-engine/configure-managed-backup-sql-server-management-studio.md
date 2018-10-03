---
title: 配置托管的备份 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0403d34b48b74d0517aaf3cb31ea520dbc436f89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165597"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>配置托管备份 (SQL Server Management Studio)
  **托管备份**对话框可以配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]实例的默认值。 本主题介绍如何使用此对话框可以配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的实例和执行此操作时必须考虑的选项的默认设置。 当[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]配置对于实例，设置将应用于任何此后创建的新数据库。  
  
 如果你想要配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]特定的数据库，请参阅[启用和配置 SQL Server 托管备份到 Windows Azure 数据库](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
 
> [!NOTE] 
> 代理服务器不支持 SQL Server 托管备份。 
  
## <a name="task-list"></a>任务列表  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 使用函数的托管备份接口在 SQL Server Management Studio  
 在此版本中，您只能配置实例级别默认设置，请使用**管理备份**接口。 无法配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]数据库中，暂停或恢复[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]操作或设置电子邮件通知。 了解如何执行操作当前不支持通过**托管备份**接口，请参阅[SQL Server 托管备份到 Windows Azure-保持和存储设置](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
## <a name="permissions"></a>Permissions  
 **查看托管备份节点是 SQL Server Management Studio:** 以查看**托管备份**中的节点**对象资源管理器**，您必须是系统管理员或具有以下权限专门授予您的用户帐户：  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` 在`smart_admin.fn_is_master_switch_on`。  
  
-   `SELECT` 在`smart_admin.fn_backup_instance_config`。  
  
 **配置托管备份：** 若要配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在 SQL Server Management Studio，您必须是系统管理员或具有以下权限：  
  
 中的成员身份`db_backupoperator`数据库角色的`ALTER ANY CREDENTIAL`权限，并`EXECUTE`权限`sp_delete_backuphistory`存储过程。  
  
 `SELECT` 权限`smart_admin.fn_get_current_xevent_settings`函数。  
  
 `EXECUTE` 权限`smart_admin.sp_get_backup_diagnostics`存储过程。 此外，它还需要 `VIEW SERVER STATE` 权限，因为它在内部调用其他需要此权限的系统对象。  
  
 `EXECUTE` 上的权限`smart_admin.sp_set_instance_backup`，和`smart_admin.sp_backup_master_switch`。  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用 SQL Server Management Studio  
 从**对象资源管理器**，展开**管理**节点，然后右键单击**托管备份**。 选择 **“配置”**。 这将打开 **“托管备份”** 对话框。  
  
 检查**启用托管备份**选项，并指定配置值：  
  
 **文件保留**期天数为单位指定和应为介于 1 和 30 之间。  
  
 **的 SQL 凭据**您选择应与存储帐户。 如果你当前没有存储身份验证信息的 SQL 凭据，则可以创建一个通过单击**创建**。 你还可以通过使用 CREATE CREDENTIAL Transact-SQL 语句创建凭据，并提供用于身份识别的存储帐户名和用于 SECRET 参数的访问密钥。 有关详细信息，请参阅[创建凭据](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential)。  
  
 指定**存储 URL**为 Windows Azure 存储帐户，存储为存储帐户的身份验证信息和备份文件的保留期的 SQL 凭据。  
  
 存储 URL 格式： https://\<存储帐户 >.blob.core.windows.net/  
  
 若要在实例级别设置的加密设置，请检查**加密备份**选项，并指定算法和证书或非对称密钥用于加密。  以实例级别设置的此值将用于应用此配置后创建的所有新数据库。  
  
> [!WARNING]  
>  不能使用此对话框来指定加密选项，而无需配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 这些加密选项仅适用于[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]操作。 若要为其他备份过程使用加密，请参阅[备份加密](../relational-databases/backup-restore/backup-encryption.md)。  
  
### <a name="considerations"></a>注意事项  
 如果配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在实例级别的设置应用于任何此后创建的新数据库。  然而，现有数据库将不会自动继承这些设置。 若要配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]以前存在的数据库，必须专门配置每个数据库。 有关详细信息，请参阅[启用和配置 SQL Server 托管备份到 Windows Azure 数据库](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
  
 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已暂停使用`smart_admin.sp_backup_master_switch`，您将看到一条警告消息"托管备份处于禁用状态和当前配置将不会生效..." 。 使用`smart_admin.sp_backup_master_switch`存储和设置@new_state= 1。 这将恢复[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]服务和配置设置将生效。 存储过程的详细信息，请参阅[smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [针对 Microsoft Azure 的 SQL Server 托管备份：互操作性和共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
