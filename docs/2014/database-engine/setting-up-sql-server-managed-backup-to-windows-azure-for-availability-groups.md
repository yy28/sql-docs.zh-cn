---
title: 为可用性组设置 SQL Server Managed Backup to Windows Azure |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8a367b7835b08c9a5b2b7226b8f3e4d127235487
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126147"
---
# <a name="setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups"></a>为可用性组设置 SQL Server 托管备份到 Windows Azure
  本主题是有关为参与 AlwaysOn 可用性组的数据库配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的教程。  
  
## <a name="availability-group-configurations"></a>可用性组配置  
 对于可用性组数据库，无论副本是全部本地配置的、在 Windows Azure 上整个配置的还是在本地配置和一个或多个 Windows Azure 虚拟机之间混合实现的，都支持 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 不过，对于一个或多个实现，可能需要考虑以下方面：  
  
-   日志备份频率：日志备份频率是时间和日志增长。 例如，日志每两小时备份一次，除非两小时内使用的日志空间为 5 MB 或更多。 这适用于所有实现，包括本地、云或混合实现。  
  
-   网络带宽：这适用于副本位于不同物理位置的实现（例如混合云）或仅有云的配置中跨不同 Windows Azure 区域的实现。 如果副本设置为同步复制，网络带宽会影响副本的滞后时间，这又可能导致主副本的日志增长。 如果副本设置为同步复制，由于网络滞后时间，副本可能无法保持同步，这在故障转移到辅助副本时可能导致数据丢失。  
  
### <a name="configuring-includesssmartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>为可用性数据库配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 **权限：**  
  
-   要求的成员身份**db_backupoperator**与数据库角色， **ALTER ANY CREDENTIAL**权限，和`EXECUTE`权限**sp_delete_backuphistory**存储过程。  
  
-   需要**选择**权限**smart_admin.fn_get_current_xevent_settings**函数。  
  
-   需要`EXECUTE`权限**smart_admin.sp_get_backup_diagnostics**存储过程。 此外，它还需要 `VIEW SERVER STATE` 权限，因为它在内部调用其他需要此权限的系统对象。  
  
-   需要`EXECUTE`权限`smart_admin.sp_set_instance_backup`和`smart_admin.sp_backup_master_switch`存储过程。  
  
 下面是为 AlwaysOn 可用性组设置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的基本步骤。 本主题后面将介绍详细的分步教程。  
  
1.  创建可用性组后，配置首选备份副本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 也会使用可用性组的这个设置来确定将哪个副本用于备份。 有关如何设置的备份首选项的分步说明，请参阅[可用性副本上配置备份&#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。  如果要创建一个新的 AlwaysOn 可用性组，请参阅[Getting Started with AlwaysOn 可用性组&#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)。  
  
2.  配置对辅助副本的只读连接访问。 有关分步说明有关如何配置只读访问，请参阅[配置对可用性副本的只读访问&#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
3.  指定备份副本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 使用首选备份副本设置决定使用哪个数据库安排从它进行备份。  若要确定当前副本是否为首选备份副本，请使用[sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函数。  
  
4.  在运行每个副本上[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]数据库使用的配置**智能 admin.sp_set_db_backup**存储过程。  
  
     **[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 故障转移后的行为：** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]将继续工作并维护故障转移事件之后的备份副本和可恢复性。 故障转移后不需要执行任何特定操作。  
  
#### <a name="considerations-and-requirements"></a>注意事项和要求：  
 为参与 AlwaysOn 可用性组的数据库配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 需要考虑特定的事项并且有特定的要求。 下面列出了注意事项和要求：  
  
-   对于参与同一可用性组的所有 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 节点上的所有数据库，各项 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置设置都应该相同。 要想实现此目标，您可以在数据库级别为主要副本和所有其他副本设置相同的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 配置，也可以在参与可用性组的所有节点上设置相同的默认 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 设置。 我们建议在数据库级别设置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，因为在数据库级别配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 可将设置与数据库隔离，因此更改默认设置只会影响实例上的所有其他数据库。  
  
-   指定备份副本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 使用首选备份副本设置安排备份。 若要确定当前副本是否为首选备份副本，请使用[sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函数。  
  
-   如果将辅助副本配置为首选副本，则至少应为它配置只读连接访问权限。 不支持对辅助数据库没有连接访问权限的可用性组。  有关详细信息，请参阅 [配置对可用性副本的只读访问 (SQL Server)](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
-   如果您在配置完可用性组后配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 会尝试复制任何现有备份，并将它们复制到存储容器中。  如果 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 找不到或不能访问现有备份，它将安排一次完整数据库备份。 这是为了优化可用性组数据库的备份操作而专门进行的。  
  
-   如果新建可用性数据库，但不想将实例级别设置应用于该数据库，则可能要考虑禁用实例级别设置  
  
-   当使用加密时，对所有副本使用相同的证书。 这有助于在故障转移或还原到不同副本时保持连续不间断的备份操作。  
  
#### <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>为可用性数据库启用和配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 本教程首先介绍为计算机 Node1 和 Node2 上的数据库 (AGTestDB) 启用和配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的步骤，然后介绍允许监视 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 运行状况的步骤。  
  
1.  **创建 Windows Azure 存储帐户：** 备份存储在 Windows Azure Blob 存储服务。 如果您没有 Windows Azure 存储帐户，必须首先创建一个。 有关详细信息，请参阅[创建 Windows Azure 存储帐户](http://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)。 记录下存储帐户的名称、访问密钥和存储帐户的 URL。 存储帐户名称和访问密钥用于创建 SQL 凭据。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 在备份操作期间使用 SQL 凭据对存储帐户进行身份验证。  
  
2.  **创建 SQL 凭据：** 创建 SQL 凭据使用的存储帐户的名称作为标识和存储访问密钥作为密码。  
  
3.  **确保 SQL Server 代理服务启动且正在运行：** 如果当前未运行 SQL Server 代理，则启动它。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 需要实例上运行有 SQL Server 代理才能执行备份操作。  可能要将 SQL 代理设置为自动运行以确保可正常进行备份操作。  
  
4.  **确定保持期：** 确定要用于备份文件的保持期。 以天为单位指定保持期，范围可为 1 到 30。 保持期决定了可恢复数据库的时段。  
  
5.  **创建证书或非对称密钥用于加密过程后：** 在节点 1，第一个节点上创建证书，然后将其导出为文件使用[备份证书&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)... 在 Node 2 上，使用从 Node 1 导出的文件创建证书。 从文件创建证书的详细信息，请参阅中的示例[创建证书&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)。  
  
6.  **启用和配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]有关在节点 1 上的 AGTestDB:** 启动 SQL Server Management Studio 并连接到可用性数据库的安装位置的节点 1 上的实例。 在根据要求修改数据库名称、存储 URL、SQL 凭据和保持期的值后，从查询窗口中运行以下语句：  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     有关创建加密证书的详细信息，请参阅**创建备份证书**中步骤[Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)。  
  
7.  **启用和配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]为 AGTestDB 上 Node2:** 启动 SQL Server Management Studio 并连接到 Node2 可用性数据库的安装位置上的实例。 在根据要求修改数据库名称、存储 URL、SQL 凭据和保持期的值后，从查询窗口中运行以下语句：  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 数据库上的备份操作最多可能需要 15 分钟才能运行。 备份将在首选备份副本上进行。  
  
8.  **查看扩展事件默认配置：** 通过在副本上运行以下 TRANSACT-SQL 语句查看扩展的事件配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用于计划的备份。 这通常是数据库所属可用性组的首选备份副本设置。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     应看到默认情况下启用管理、操作和分析通道事件，且无法禁用这些事件。 这对于需要手动干预的事件来说应当已经足够。  您可以启用调试事件，但是这些通道包含 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 用来检测问题和解决问题的信息性事件和调试事件。 有关详细信息，请参阅[监视器 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
9. **启用和配置运行状况的通知：**[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 有一个存储过程，它创建代理作业以发出可能需要注意的错误或警告的电子邮件通知。  若要接收此类通知，必须允许运行这个创建 SQL Server 代理作业的存储过程。 以下步骤说明了启用和配置电子邮件通知的过程：  
  
    1.  如果尚未在此实例上启用数据库邮件，请进行设置。 有关详细信息，请参阅 [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)。  
  
    2.  将 SQL Server 代理通知配置为使用数据库邮件。 有关详细信息，请参阅 [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **启用电子邮件通知以接收备份错误和警告：** 从查询窗口中，运行以下 Transact-SQL 语句：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         有关详细信息和一个完整的示例脚本，请参阅[监视器 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
10. **在 Windows Azure 存储帐户中查看备份文件：** 从 SQL Server Management Studio 或 Azure 管理门户连接到存储帐户。 您将看到一个 SQL Server 实例的容器，其中承载您配置为使用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的数据库。 您也会在为数据库启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的 15 分钟内，看到数据库和日志备份。  
  
11. **监视运行状态：**  你可以通过以前配置的电子邮件通知进行监视，也可以主动监控记录的事件。 以下是一些用于查看事件的示例 Transact-SQL 语句：  
  
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
    event varchar (512),  
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
  
 本节中描述的步骤是专门用于在数据库上首次配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 你可以修改使用相同的系统存储过程的现有配置**smart_admin.sp_set_db_backup** ，提供新值。 有关详细信息，请参阅[SQL Server Managed Backup to Windows Azure-保持和存储设置](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>从 AlwaysOn 可用性组删除数据库时的注意事项  
 如果数据库从 AlwaysOn 可用性组配置中删除，并且现在是一个独立的数据库，我们建议执行操作备份使用[smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)。 采用这种方式创建数据库备份时，将建立一个新的备份链，而文件将被放入实例特定的容器而非可用性容器中，当数据库是可用性组的一部分时，数据库存储在可用性容器中。  
  
> [!WARNING]  
>  无法保证在可用性组状态更改之前可在此场景下从备份恢复数据库。  
  
  
