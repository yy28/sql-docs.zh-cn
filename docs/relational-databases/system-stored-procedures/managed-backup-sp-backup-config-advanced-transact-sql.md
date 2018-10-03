---
title: managed_backup.sp_backup_config_advanced (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3f19fed072e693de6bbebb53354eae8c0bfaa0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827905"
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  配置高级的设置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> 参数  
 @database_name  
 启用托管的备份上特定数据库的数据库名称。 如果为 NULL 或 *，则此托管的备份适用于服务器上的所有数据库。  
  
 @encryption_algorithm  
 备份过程中用于加密备份文件的加密算法的名称。 @encryption_algorithm是**SYSNAME**。 在首次为数据库配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 时，它是必需的参数。 指定**NO_ENCRYPTION**如果不希望加密备份文件。 在更改 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 配置设置时，此参数是可选参数；如果不指定，则会保留现有的配置值。 为此参数允许的值为：  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 有关加密算法的详细信息，请参阅 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)。  
  
 @encryptor_type  
 加密程序，可以是任一证书的类型或 ASYMMETRIC_KEY"。 @encryptor_type是**nvarchar （32)**。 此参数是可选的如果指定为 NO_ENCRYPTION@encryption_algorithm参数。  
  
 @encryptor_name  
 要用于加密备份的现有证书或非对称密钥的名称。 @encryptor_name是**SYSNAME**。 如果使用非对称密钥，则必须使用扩展密钥管理 (EKM) 进行配置。 此参数是可选的如果指定为 NO_ENCRYPTION@encryption_algorithm参数。  
  
 有关详细信息，请参阅[可扩展的密钥管理 (EKM)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
 @local_cache_path  
 尚不支持此参数。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求的成员身份**db_backupoperator**数据库角色的**ALTER ANY CREDENTIAL**权限，并且**EXECUTE**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="examples"></a>示例  
 下面的示例设置的高级的配置选项[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]对于 SQL Server 实例。  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
