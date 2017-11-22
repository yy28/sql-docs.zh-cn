---
title: "RESTORE HEADERONLY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
caps.latest.revision: "95"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5ea17d9f848a47639b748e6f243f604e0e3e2bb2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restore-statements---headeronly-transact-sql"></a>还原语句的 HEADERONLY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中特定备份设备上所有备份集的所有备份标头信息的结果集。  
  
> [!NOTE]  
>  自变量的说明，请参阅[RESTORE 参数 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>参数  
 RESTORE HEADERONLY 参数的说明，请参阅[RESTORE 参数 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>结果集  
 对于给定设备上的每个备份，服务器均发送一行包含以下各列的标头信息：  
  
> [!NOTE]  
>  RESTORE HEADERONLY 会查看介质上的所有备份集。 因此，使用高容量磁带机时，生成此结果集可能需要一些时间。 若要获取快速了解一下媒体而不获取有关每个备份集的信息，请使用 RESTORE LABELONLY 或指定文件 **=**  *backup_set_file_number*。  
  
> [!NOTE]  
>  由于的性质[!INCLUDE[msCoName](../../includes/msconame-md.md)]磁带格式，它不是可能的备份集从其他软件程序以占据相同的介质上的空间[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份集。 在由 RESTORE HEADERONLY 返回的结果集中，每一个来自其他软件程序的备份集都占用一行。  
  
|列名|数据类型|SQL Server 备份集说明|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar （128)**|备份集名称。|  
|**BackupDescription**|**nvarchar(255)**|备份集说明。|  
|**BackupType**|**int**|备份类型：<br /><br /> **1** = 数据库<br /><br /> **2** = 事务日志<br /><br /> **4** = 文件<br /><br /> **5** = 差异数据库<br /><br /> **6** = 差异文件<br /><br /> **7** = 部分<br /><br /> **8** = 差异部分|  
|**到期日期**|**datetime**|备份集的过期时间。|  
|**压缩**|**BYTE(1)**|是否使用基于软件的压缩对备份集进行压缩：<br /><br /> **0** = 否<br /><br /> **1** = yes|  
|**位置**|**int**|备份集在卷中的位置（用于 FILE = 选项）。|  
|**DeviceType**|**tinyint**|与用于备份操作的设备对应的编号：<br /><br /> 磁盘：<br /><br /> **2** = 逻辑<br /><br /> **102** = 物理<br /><br /> 磁带：<br /><br /> **5** = 逻辑<br /><br /> **105** = 物理<br /><br /> 虚拟设备：<br /><br /> **7** = 逻辑<br /><br /> **107** = 物理<br /><br /> 逻辑设备名称和设备号位于**sys.backup_devices**; 有关详细信息，请参阅[sys.backup_devices &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md).|  
|**UserName**|**nvarchar （128)**|执行备份操作的用户名。|  
|**ServerName**|**nvarchar （128)**|写入备份集的服务器名称。|  
|**DatabaseName**|**nvarchar （128)**|已备份的数据库名称。|  
|**DatabaseVersion**|**int**|从其中创建备份的数据库的版本。|  
|**DatabaseCreationDate**|**datetime**|数据库的创建日期和时间。|  
|**BackupSize**|**numeric(20,0)**|备份大小（以字节为单位）。|  
|**FirstLSN**|**numeric(25,0)**|备份集中第一个日志记录的日志序列号。|  
|**LastLSN**|**numeric(25,0)**|备份集之后的下一条日志记录的日志序列号。|  
|**CheckpointLSN**|**numeric(25,0)**|创建备份时最后一个检查点的日志序号。|  
|**DatabaseBackupLSN**|**numeric(25,0)**|最近的数据库完整备份的日志序列号。<br /><br /> **DatabaseBackupLSN**是"开始的检查点"，都将触发备份启动时。 此 LSN 与将同时发生**FirstLSN**如果执行备份，当数据库处于空闲状态并配置没有复制。|  
|**BackupStartDate**|**datetime**|备份操作的开始日期和时间。|  
|**BackupFinishDate**|**datetime**|备份操作的完成日期和时间。|  
|**SortOrder**|**int**|服务器排列次序。 该列仅对数据库备份有效。 提供该列是为了向后兼容。|  
|**CodePage**|**int**|服务器使用的服务器代码页或字符集。|  
|**UnicodeLocaleId**|**int**|用于 Unicode 字符数据排序的服务器 Unicode 区域设置 ID 配置选项。 提供该列是为了向后兼容。|  
|**UnicodeComparisonStyle**|**int**|服务器 Unicode 比较风格配置选项，可提供对 Unicode 数据排序的额外控制。 提供该列是为了向后兼容。|  
|**CompatibilityLevel**|**tinyint**|从其中创建备份的数据库兼容级别设置。|  
|**SoftwareVendorId**|**int**|软件供应商标识号。 对于 SQL Server，该号码是**4608** (或十六进制**0x1200**)。|  
|**SoftwareVersionMajor**|**int**|创建备份集的服务器主要版本号。|  
|**SoftwareVersionMinor**|**int**|创建备份集的服务器次要版本号。|  
|**SoftwareVersionBuild**|**int**|创建备份集的服务器内部版本号。|  
|**MachineName**|**nvarchar （128)**|执行备份操作的计算机名称。|  
|**标志**|**int**|个人标志位含义，如果设置为**1**:<br /><br /> **1** = 日志备份包含大容量日志操作。<br /><br /> **2** = 快照备份。<br /><br /> **4** = 数据库是只读的备份时。<br /><br /> **8** = 数据库处于单用户模式下备份时。<br /><br /> **16** = 备份包含备份校验和。<br /><br /> **32** = 数据库已损坏时备份，但请求备份操作错误时仍继续。<br /><br /> **64** = 结尾日志备份。<br /><br /> **128** = 具有不完整元数据的结尾日志备份。<br /><br /> **256** = 结尾日志备份使用 with NORECOVERY。<br /><br /> **重要说明：**我们建议，而不是**标志**使用单独的布尔值列 (下面开头列出**HasBulkLoggedData**结束**IsCopyOnly**)。|  
|**BindingID**|**uniqueidentifier**|数据库的绑定 ID。 这对应于**sys.database_recovery_status***database_guid**。 恢复数据库时，会分配一个新值。 另请参阅**FamilyGUID** （下文）。|  
|**RecoveryForkID**|**uniqueidentifier**|结尾恢复分支的 ID。 此列对应于**last_recovery_fork_guid**中[backupset](../../relational-databases/system-tables/backupset-transact-sql.md)表。<br /><br /> 对于数据的备份， **RecoveryForkID**等于**FirstRecoveryForkID**。|  
|**排序规则**|**nvarchar （128)**|数据库使用的排序规则。|  
|**FamilyGUID**|**uniqueidentifier**|创建时的原始数据库 ID。 恢复数据库时，此值保持不变。|  
|**HasBulkLoggedData**|**bit**|**1** = 包含大容量日志操作的日志备份。|  
|**IsSnapshot**|**bit**|**1** = 快照备份。|  
|**IsReadOnly**|**bit**|**1** = 数据库是只读的备份时。|  
|**IsSingleUser**|**bit**|**1** = 数据库处于单用户备份时。|  
|**HasBackupChecksums**|**bit**|**1** = 备份包含备份校验和。|  
|**IsDamaged**|**bit**|**1** = 数据库已损坏时备份，但请求备份操作错误时仍继续。|  
|**BeginsLogChain**|**bit**|**1** = 这是连续的日志备份链中的第一个。 日志链的开始处是创建数据库后所做的第一个日志备份，或者是数据库从简单模式切换到完整模式或大容量日志恢复模式时所做的第一个日志备份。|  
|**HasIncompleteMetaData**|**bit**|**1** = 不完整的元数据的结尾日志备份。<br /><br /> 有关具有不完整的备份元数据的结尾日志备份的信息，请参阅[结尾日志备份 &#40;SQL server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).|  
|**IsForceOffline**|**bit**|**1** = with NORECOVERY; 执行备份数据库脱机备份。|  
|**IsCopyOnly**|**bit**|**1** = 仅复制备份。<br /><br /> 仅复制备份不会影响数据库的总体备份和恢复进程。 有关详细信息，请参阅[仅复制备份 (SQL Server)](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。|  
|**FirstRecoveryForkID**|**uniqueidentifier**|起始恢复分支的 ID。 此列对应于**first_recovery_fork_guid**中[backupset](../../relational-databases/system-tables/backupset-transact-sql.md)表。<br /><br /> 对于数据的备份， **FirstRecoveryForkID**等于**RecoveryForkID**。|  
|**ForkPointLSN**|**numeric(25,0)** NULL|如果**FirstRecoveryForkID**是否不等于**RecoveryForkID**，这是分叉点的日志序列号。 否则，此值为 NULL。|  
|**RecoveryModel**|**nvarchar(60)**|数据库的恢复模式，可以是下列值之一：<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|对于单基于差异备份，则值等于**FirstLSN**的差异基准; 更改，Lsn 大于或等于**DifferentialBaseLSN**纳入差异。<br /><br /> 对于多基准的差异备份，该值为 NULL，基准 LSN 必须在文件级别确定。 有关详细信息，请参阅 [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。<br /><br /> 对于非差异备份类型，该值始终为 NULL。<br /><br /> 有关详细信息，请参阅 [差异备份 (SQL Server)](../../relational-databases/backup-restore/differential-backups-sql-server.md)。|  
|**DifferentialBaseGUID**|**uniqueidentifier**|对于单基准的差异备份，该值为差异基准的唯一标识符。<br /><br /> 对于多基准差异，此值为 NULL，且必须确定每个文件的差异基准。<br /><br /> 对于非差异备份类型，此值为 NULL。|  
|**BackupTypeDescription**|**nvarchar(60)**|字符串形式的备份类型有以下几种：<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** NULL|备份集的唯一标识号，可以根据此标识号在介质上标识备份集。|  
|**CompressedBackupSize**|**bigint**|备份集的字节计数。 对于未压缩备份，此值等同于**BackupSize**。<br /><br /> 若要计算的压缩率，请使用**CompressedBackupSize**和**BackupSize**。<br /><br /> 期间**msdb**升级，此值设置为与值匹配的**BackupSize**列。|  
|**包含**|**tinyint**不为 NULL|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指示数据库的包含状态。<br /><br /> 0 = 数据库包含状态为 OFF<br /><br /> 1 = 数据库处于部分包含状态|  
|**KeyAlgorithm**|**nvarchar(32)**|**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至当前版本。<br /><br /> 用于加密备份的加密算法。 NO_Encryption 指示备份未加密。 当无法确定正确的值时，此值应为 NULL。|  
|**EncryptorThumbprint**|**varbinary(20)**|**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至当前版本。<br /><br /> 可用于在数据库中查找证书或非对称密钥的加密程序的指纹。 当备份未加密时，此值为 NULL。|  
|**EncryptorType**|**nvarchar(32)**|**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至当前版本。<br /><br /> 使用的加密程序的类型：证书或非对称密钥。 当备份未加密时，此值为 NULL。|  
  
> [!NOTE]  
>  如果为备份集指定了密码，则 RESTORE HEADERONL 只显示其密码与命令中指定的 PASSWORD 选项相匹配的备份集的完整信息。 RESTORE HEADERONLY 还显示没有密码保护的备份集的完整信息。 **BackupName**列在媒体上的其他受密码保护的备份设置为将设置为 * * * 受密码保护\*\*\*，和所有其他列均为 NULL。  
  
## <a name="general-remarks"></a>一般备注  
 客户端可以使用 RESTORE HEADERONLY 检索特殊备份设备上的所有备份的所有备份标头信息。 对于备份设备上的每个备份，服务器都会将标头信息作为一行发送。  
  
## <a name="security"></a>安全性  
 在备份时，可以根据需要为介质集、备份集或这两者指定密码。 如果已经在介质集或备份集上定义了密码，则必须在 RESTORE 语句中指定正确的密码。 这些密码防止未经授权的还原操作，并且未授权的媒体使用的备份集追加[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]工具。 但是，密码不会阻止使用 BACKUP 语句的 FORMAT 选项覆盖介质。  
  
> [!IMPORTANT]  
>  此密码提供的安全性较低。 它旨在防止经过授权的用户或未经授权的用户使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具执行不正确的还原操作。 但是不能防止通过其他方式或通过替换密码来读取备份数据。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]保护备份的最佳做法是在一个安全位置或备份到磁盘保护的文件，由足够的访问控制列表 (Acl) 来存储备份的磁带。 ACL 应设置在创建备份的根目录下。  
  
### <a name="permissions"></a>Permissions  
 获取有关备份集或备份设备的信息需要具有 CREATE DATABASE 权限。 有关详细信息，请参阅 [GRANT 数据库权限 (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 以下示例返回磁盘文件 `C:\AdventureWorks-FullBackup.bak` 标头中的信息。  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY (Transact-SQL)](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)   
 [备份历史记录和标头信息 (SQL Server)](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [启用或禁用备份校验和在备份或还原 &#40; 过程SQL server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [媒体集、媒体簇和备份集 (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [恢复模式 (SQL Server)](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
