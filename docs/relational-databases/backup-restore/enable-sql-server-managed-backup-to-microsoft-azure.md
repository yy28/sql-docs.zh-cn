---
title: "启用 SQL Server Managed Backup to Microsoft Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3d5227792c9f1a658135e1efa5c00bbcfe078cfe
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>对 Microsoft Azure 启用 SQL Server 托管备份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题介绍如何在数据库级别和实例级别使用默认设置以启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 还介绍了如何启用电子邮件通知以及如何监视备份活动。  
  
 本教程使用 Azure PowerShell。 教程开始前， [请下载并安装 Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)。  
  
> [!IMPORTANT]  
>  如果想启用高级选项或使用自定义计划，请在启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前先配置这些设置。 有关详细信息，请参阅 [配置 SQL Server Managed Backup to Microsoft Azure 的高级选项](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)。  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>使用默认设置启用并配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
#### <a name="create-the-azure-blob-container"></a>创建 Azure Blob 容器  
  
1.  **注册 Azure：** 如果已经有 Azure 订阅，请转到下一步。 如果没有，可以使用 [免费试用版](http://azure.microsoft.com/pricing/free-trial/) 开始，或者浏览 [购买选项](http://azure.microsoft.com/pricing/purchase-options/)。  
  
2.  **创建 Azure 存储帐户：** 如果已经有存储帐户，请转到下一步。 如果没有，可以使用 [Azure 管理门户](https://manage.windowsazure.com/) 或者 Azure PowerShell 来创建存储帐户。 以下 `New-AzureStorageAccount` 命令在美国东部地区创建了一个名为 `managedbackupstorage` 的存储帐户。  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     有关存储帐户的详细信息，请参阅 [关于 Azure 存储帐户](http://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account/)。  
  
3.  **创建备份文件的 Blob 容器：** 可以在 Azure 管理门户中或者使用 Azure PowerShell 创建 Blob 容器。 以下 `New-AzureStorageContainer` 命令在 `backupcontainer` 存储帐户中创建了一个名为 `managedbackupstorage` 的 Blob 容器。  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **生成共享访问签名 (SAS)：** 要访问容器，必须创建 SAS。 使用某些工具、代码和 Azure PowerShell 可以完成此操作。 以下 `New-AzureStorageContainerSASToken` 命令为一年后过期的 `backupcontainer` Blob 容器创建 SAS 令牌。  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
    New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
    ```  
  
     此命令的输出将包含容器的 URL 和 SAS 令牌。 以下是一个示例：  
  
    ```  
    https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl  
    ```  
  
     上述示例中，容器 URL 从问号处的 SAS 令牌（不包括问号）分隔开来。 例如，前面的输出会得出以下两个值。  
  
    |||  
    |-|-|  
    |**容器 URL：**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
    |**SAS 令牌：**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
  
     将容器 URL 和 SAS 记录下来，以便在创建 SQL 凭据时使用。 有关 SAS 的详细信息，请参阅 [共享访问签名，第一部分：了解 SAS 模型](http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **创建 SAS URL 的 SQL 凭据：** 使用 SAS 令牌来创建 Blob 容器 URL 的 SQL 凭据。 在 SQL Server Management Studio 中，使用下列 Transact-SQL 查询来创建 Blob 容器 URL 的凭据，示例如下：  
  
    ```tsql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **确保 SQL Server 代理服务启动且正在运行：** 如果当前未运行 SQL Server 代理，则启动它。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要实例上运行有 SQL Server 代理才能执行备份操作。  可能要将 SQL Server 代理设置为自动运行，以确保可定期进行备份操作。  
  
3.  **确定保持期：** 确定备份文件的保持期。 以天为单位指定保持期，范围可为 1 到 30。  
  
4.  **Enable and configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ：** 启动 SQL Server Management Studio 并连接到目标 SQL Server 实例。 在根据要求修改数据库名称、容器 URL 和保持期的值后，从查询窗口中运行以下语句：  
  
    > [!IMPORTANT]  
    >  若要在实例级别启用托管备份，请为 `NULL` 参数指定 `database_name` 。  
  
    ```tsql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 数据库上的备份操作最多可能需要 15 分钟才能运行。  
  
5.  **检查扩展事件默认配置：** 通过运行以下 transact-SQL 语句，检查扩展事件配置。  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     应看到默认情况下启用管理、操作和分析通道事件，且无法禁用这些事件。 这对于需要手动干预的事件来说应当已经足够。  您可以启用调试事件，但是调试通道包含 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 用来检测问题和解决问题的信息性事件和调试事件。  
  
6.  **启用和配置运行状况的通知：**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 有一个存储过程，它创建代理作业以发出可能需要注意的错误或警告的电子邮件通知。 以下步骤说明了启用和配置电子邮件通知的过程：  
  
    1.  如果尚未在此实例上启用数据库邮件，请进行设置。 有关详细信息，请参阅 [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md)。  
  
    2.  将 SQL Server 代理通知配置为使用数据库邮件。 有关详细信息，请参阅 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **启用电子邮件通知以接收备份错误和警告：** 从查询窗口中，运行以下 Transact-SQL 语句：  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **在 Microsoft Azure 存储帐户中查看备份文件：** 从 SQL Server Management Studio 或 Azure 管理门户中连接到存储帐户。 你将在指定容器中看到任何备份文件。 请注意，你会在启用数据库的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的 5 分钟内看到数据库和日志备份。  
  
8.  **监视运行状态：**  你可以通过以前配置的电子邮件通知进行监视，也可以主动监控记录的事件。 以下是一些用于查看事件的示例 Transact-SQL 语句：  
  
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
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 本节中描述的步骤是专门用于在数据库上首次配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 你可以使用相同的系统存储过程来修改现有配置，并提供新值。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
