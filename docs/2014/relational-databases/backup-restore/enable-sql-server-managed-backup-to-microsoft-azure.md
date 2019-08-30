---
title: 设置 SQL Server 托管备份到 Azure |Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b69439226b55965e37f24f2131c77340ae833590
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154726"
---
# <a name="setting-up-sql-server-managed-backup-to-azure"></a>设置 SQL Server 托管备份到 Azure
  本主题包括两个教程：  
  
 在数据库级别设置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、启用电子邮件通知和监视备份活动。  
  
 在实例级别设置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、启用电子邮件通知和监视备份活动。  
  
 有关为可用性组设置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的教程, 请参阅为[可用性组 Microsoft Azure 设置 SQL Server 托管备份](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)。  
  
## <a name="setting-up-includess_smartbackupincludesss-smartbackup-mdmd"></a>设置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-a-database"></a>为数据库启用和配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 本教程首先介绍为数据库 (TestDB) 启用和配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]所需的步骤，然后介绍允许监视 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]运行状况的步骤。  
  
 **权限：**  
  
-   要求具有**db_backupoperator**数据库角色的成员身份, 具有**ALTER ANY CREDENTIAL** `EXECUTE`权限以及对**sp_delete_backuphistory**存储过程的权限。  
  
-   需要对**smart_admin. fn_get_current_xevent_settings**函数的**SELECT**权限。  
  
-   需要`EXECUTE`对 smart_admin 的**sp_get_backup_diagnostics**存储过程的权限。 此外，它还需要 `VIEW SERVER STATE` 权限，因为它在内部调用其他需要此权限的系统对象。  
  
-   需要`EXECUTE`对`smart_admin.sp_set_instance_backup` 和`smart_admin.sp_backup_master_switch`存储过程的权限。  


1.  **创建 Microsoft Azure 的存储帐户:** 备份存储在 Microsoft Azure 存储服务中。 如果还没有帐户, 则必须先创建一个 Microsoft Azure 的存储帐户。
    - SQL Server 2014 使用不同于块 blob 和追加 blob 的页 blob。 因此, 您必须创建一个常规用途帐户, 而不是一个 blob 帐户。 有关详细信息, 请参阅[关于 Azure 存储帐户](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。
    - 请记录存储帐户名称和访问密钥。 存储帐户名称和访问密钥用于创建 SQL 凭据。 使用 SQL 凭据对存储帐户进行身份验证。  
 
2.  **创建 SQL 凭据:** 使用存储帐户的名称作为标识, 并使用存储访问密钥作为密码创建 SQL 凭据。  
  
3.  **确保 SQL Server 代理服务已启动且正在运行：** 如果 SQL Server 代理当前未运行，请启动它。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要实例上运行有 SQL Server 代理才能执行备份操作。  可能要将 SQL Server 代理设置为自动运行，以确保可定期进行备份操作。  
  
4.  **确定保持期：** 确定备份文件的保持期。 以天为单位指定保持期，范围可为 1 到 30。  
  
5.  **启用和配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：** 开始 SQL Server Management Studio 然后连接到安装了数据库的实例。 在根据要求修改数据库名称、SQL 凭据、保持期和加密选项的值后，从查询窗口中运行以下语句：  
  
     有关创建用于加密的证书的详细信息, 请参阅[创建加密的备份](create-an-encrypted-backup.md)中的**创建备份证书**步骤。  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 数据库上的备份操作最多可能需要 15 分钟才能运行。  
  
6.  **查看扩展事件默认配置：** 通过运行以下 transact-SQL 语句，检查扩展事件设置。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     应看到默认情况下启用管理、操作和分析通道事件，且无法禁用这些事件。 这对于需要手动干预的事件来说应当已经足够。  您可以启用调试事件，但是调试通道包含 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 用来检测问题和解决问题的信息性事件和调试事件。 有关详细信息, 请参阅[监视 SQL Server 托管备份到 Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
7.  **启用和配置运行状况的通知：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 有一个存储过程，它创建代理作业以发出可能需要注意的错误或警告的电子邮件通知。 以下步骤说明了启用和配置电子邮件通知的过程：  
  
    1.  如果尚未在此实例上启用数据库邮件，请进行设置。 有关详细信息，请参阅 [Configure Database Mail](../database-mail/configure-database-mail.md)。  
  
    2.  将 SQL Server 代理通知配置为使用数据库邮件。 有关详细信息，请参阅 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **启用电子邮件通知以接收备份错误和警告：** 在查询窗口中，运行以下 Transact-SQL 语句：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         有关详细信息和完整的示例脚本, 请参阅[监视 SQL Server 托管备份到 Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
8.  **查看 Microsoft Azure 存储帐户中的备份文件：** 从 SQL Server Management Studio 或 Azure 管理门户连接到存储帐户。 您将看到一个 SQL Server 实例的容器，其中承载您配置为使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的数据库。 您也会在为数据库启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的 15 分钟内，看到数据库和日志备份。  
  
9. **监视运行状态：** 可以通过以前配置的电子邮件通知进行监视，也可以主动监控记录的事件。 以下是一些用于查看事件的示例 Transact-SQL 语句：  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 本节中描述的步骤是专门用于在数据库上首次配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 您可以使用相同的系统存储过程**smart_admin**来修改现有配置, 并提供新的值。 有关详细信息, 请参阅[SQL Server 托管备份到 Microsoft Azure 保留和存储设置](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
### <a name="enable-includess_smartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>使用默认设置为实例启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 本教程介绍为实例 "MyInstance [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] \\" 启用和配置的步骤。 其中包括允许监视 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 运行状况的步骤。  
  
 **权限：**  
  
-   要求具有**db_backupoperator**数据库角色的成员身份, 具有**ALTER ANY CREDENTIAL** `EXECUTE`权限以及对**sp_delete_backuphistory**存储过程的权限。  
  
-   需要对**smart_admin. fn_get_current_xevent_settings**函数的**SELECT**权限。  
  
-   需要`EXECUTE`对 smart_admin 的**sp_get_backup_diagnostics**存储过程的权限。 此外，它还需要 `VIEW SERVER STATE` 权限，因为它在内部调用其他需要此权限的系统对象。  


1.  **创建 Microsoft Azure 的存储帐户:** 备份存储在 Microsoft Azure 存储服务中。 如果还没有帐户, 则必须先创建一个 Microsoft Azure 的存储帐户。
    - SQL Server 2014 使用不同于块 blob 和追加 blob 的页 blob。 因此, 您必须创建一个常规用途帐户, 而不是一个 blob 帐户。 有关详细信息, 请参阅[关于 Azure 存储帐户](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。
    - 请记录存储帐户名称和访问密钥。 存储帐户名称和访问密钥用于创建 SQL 凭据。 使用 SQL 凭据对存储帐户进行身份验证。  
  
2.  **创建 SQL 凭据:** 使用存储帐户的名称作为标识, 并使用存储访问密钥作为密码创建 SQL 凭据。  
  
3.  **确保 SQL Server 代理服务已启动且正在运行：** 如果 SQL Server 代理当前未运行，请启动它。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要实例上运行有 SQL Server 代理才能执行备份操作。  可能要将 SQL Server 代理设置为自动运行，以确保可定期进行备份操作。  
  
4.  **确定保持期：** 确定备份文件的保持期。 以天为单位指定保持期，范围可为 1 到 30。 在实例级别使用默认值启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 后，此后创建的所有新数据库将继承这些设置。 只会支持和自动配置设置为完整或大容量日志恢复模式的数据库。 如果您不想配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，您可以随时为特定数据库禁用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 还可通过在数据库级别配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，更改特定数据库的配置。  
  
5.  **启用和配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：** 启动 SQL Server Management Studio 并连接到 SQL Server 的实例。 在根据要求修改数据库名称、SQL 凭据、保持期和加密选项的值之后, 在查询窗口中运行以下语句:  
  
     有关创建用于加密的证书的详细信息, 请参阅[创建加密的备份](create-an-encrypted-backup.md)中的**创建备份证书**步骤。  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     现在，已对实例启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
6.  通过运行以下 Transact-SQL 语句验证配置设置：  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  在实例上创建新数据库。 运行以下 Transact-SQL 语句，查看数据库的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 配置设置：  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     最多可能需要 15 分钟才能显示设置，并开始运行数据库的备份操作。  
  
8.  **启用和配置运行状况的通知：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 有一个存储过程，它创建代理作业以发出可能需要注意的错误或警告的电子邮件通知。  若要接收此类通知，必须允许运行这个创建 SQL Server 代理作业的存储过程。 以下步骤说明了启用和配置电子邮件通知的过程：  
  
    1.  如果尚未在此实例上启用数据库邮件，请进行设置。 有关详细信息，请参阅 [Configure Database Mail](../database-mail/configure-database-mail.md)。  
  
    2.  将 SQL Server 代理通知配置为使用数据库邮件。 有关详细信息，请参阅 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **启用电子邮件通知以接收备份错误和警告：** 在查询窗口中，运行以下 Transact-SQL 语句：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         有关如何监视的详细信息和完整的示例脚本, 请参阅[监视 SQL Server 托管备份到 Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
9. **查看 Microsoft Azure 存储帐户中的备份文件：** 从 SQL Server Management Studio 或 Azure 管理门户连接到存储帐户。 您将看到一个 SQL Server 实例的容器，其中承载您配置为使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的数据库。 您也会在创建新数据库 15 分钟内，看到数据库和日志备份。  
  
10. **监视运行状态：** 可以通过以前配置的电子邮件通知进行监视，也可以主动监控记录的事件。 以下是一些用于查看事件的示例 Transact-SQL 语句：  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 可通过专门在数据库级别配置设置，在特定数据库中取代 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 默认设置。 您还可以临时暂停和继续运行 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服务。 有关详细信息, 请参阅[SQL Server 托管备份到 Microsoft Azure 保留和存储设置](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)  
  
  
