---
title: "配置 SQL Server Managed Backup to Microsoft Azure 的高级选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4c2bb5ecc63c0168989e6ae23c0d85d5a22dea3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>配置 SQL Server Managed Backup to Microsoft Azure 的高级选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 以下教程介绍如何设置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的高级选项。 仅当你需要提供的这些功能时，才需要这些步骤。 否则，可以启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 并依赖于默认行为。  
  
 在每个方案中，使用 `database_name` 参数指定备份。 当 `database_name` 为 NULL 或 * 时，这些更改会影响实例级别的默认设置。 实例级别的设置也会影响在更改后创建的新数据库。  
  
 指定这些设置后，便可以使用系统存储过程 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) 为数据库或实例启用托管备份。 有关详细信息，请参阅 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)。  
  
> [!WARNING]  
>  在使用 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) 启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 之前，应该始终配置高级选项和自定义计划选项。 否则，在启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 和配置这些设置之间的这一时间段中，可能会发生不需要的备份操作。  
  
## <a name="configure-encryption"></a>配置加密  
 以下步骤说明了如何使用存储过程 [managed_backup.sp_backup_config_advanced (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) 来指定加密设置。  
  
1.  **确定加密算法：** 首先确定要使用的加密算法的名称。 选择以下算法之一：  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **创建数据库主密钥：** 选择一个密码，用于加密将存储在数据库中的主密钥的副本。  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **创建备份证书或非对称密钥：** 可以将证书或非对称密钥用于加密。 以下示例创建了用于加密的备份证书。  
  
    ```tsql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **设置托管备份加密：** 使用相应的值调用 **managed_backup.sp_backup_config_advanced** 存储过程。 例如，以下示例使用名为 `MyDB` 的证书和 `MyTestDBBackupEncryptCert` 加密算法为加密配置 `AES_128` 数据库。  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  如果在上一示例中 `@database_name` 为 NULL，这些设置则应用于 SQL Server 实例。  
  
## <a name="configure-a-custom-backup-schedule"></a>配置自定义备份计划  
 以下步骤说明了如何使用存储过程 [managed_backup.sp_backup_config_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) 设置自定义计划。  
  
1.  **确定完整备份的频率：** 确定进行完整数据库备份的频率。 可以选择“每日”或“每周”完整备份。  
  
2.  **确定日志备份的频率：** 确定进行日志备份的频率。 此值以分钟或小时为单位。  
  
3.  **确定在星期几进行每周备份：** 如果是每周备份，请选择在星期几进行完整备份。  
  
4.  确定备份的开始时间：使用 24 小时表示法，选择开始备份的时间。  
  
5.  **确定允许备份的时间长度：** 这将指定必须完成备份的时间。  
  
6.  **设置自定义备份计划：** 以下存储过程为 `MyDB` 数据库定义了自定义计划。 完整备份将在每周 `Monday` 的 `17:30`进行。 每 `5` 分钟进行日志备份。 备份完成的时间为两个小时。  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>后续步骤  
 在配置高级选项和自定义计划后，必须在目标数据库或 SQL Server 实例上启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 有关详细信息，请参阅 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
