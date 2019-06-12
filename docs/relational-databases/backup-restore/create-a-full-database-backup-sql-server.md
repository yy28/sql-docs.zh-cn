---
title: 创建完整数据库备份 (SQL Server) | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 05/29/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c90a3cf1f74eb588bd6faa657a3f47d7e57df453
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403055"
---
# <a name="create-a-full-database-backup-sql-server"></a>创建完整数据库备份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建完整数据库备份。  
  

若要了解如何将 SQL Server 备份到 Azure Blob 存储服务，请参阅[使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)和 [SQL Server 备份到 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。  
  
##  <a name="Restrictions"></a> 限制和局限  
  
-   不允许在显式或隐式事务中使用 BACKUP 语句。    
-   无法在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中还原较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建的备份。   
-   有关备份概念和任务的概述和详细信息，请在继续操作前先参阅[备份概述 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)。  
  
## <a name="Recommendations"></a> 建议  
  
-   随着数据库不断增大，完整数据库备份的完成时间会延长，并且需要占用更多存储空间。 对于大型数据库，请考虑用一系列[差异数据库备份](../../relational-databases/backup-restore/differential-backups-sql-server.md)来补充完整数据库备份。 有关详细信息，请参阅 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。    
-   使用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 系统存储过程估计完整数据库备份的大小。    
-   默认情况下，每个成功的备份操作都会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和系统事件日志中添加一个条目。 若频繁备份，这些成功消息会迅速累积，从而生成巨大的错误日志！ 这会使查找其他消息变得非常困难。 在这些情况下，如果脚本均不依赖于这些备份日志条目，则可使用跟踪标志 3226 取消这些条目。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
##  <a name="Security"></a> Security  
 针对数据库备份，TRUSTWORTHY 设置为 OFF。 有关如何将 TRUSTWORTHY 设置为 ON 的详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始， **PASSWORD** 和 **MEDIAPASSWORD** 选项不再可用于创建备份。 不过，您仍可以还原使用密码创建的备份。  
  
##  <a name="Permissions"></a> 权限  
 默认情况下，为 **sysadmin** 固定服务器角色以及 **db_owner** 和 **db_backupoperator** 固定数据库角色的成员授予 BACKUP DATABASE 和 BACKUP LOG 权限。  
  
 备份设备的物理文件的所有权和权限问题可能会妨碍备份操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须能够读取和写入设备；运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户 **必须** 具有写入权限。 但是，用于在系统表中为备份设备添加项目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)不检查文件访问权限。 备份设备物理文件的这些问题可能直到为备份或还原而访问物理资源时才会出现。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定备份任务时，可以通过单击“脚本”  按钮并选择脚本目标生成相应的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 脚本。  
  
### <a name="back-up-a-database"></a>备份数据库  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例之后，在“对象资源管理器”中，单击服务器名称以展开服务器树。     
1.  展开“数据库”，选择用户数据库，或展开“系统数据库”，选择系统数据库。      
1.  右键单击数据库，指向 **“任务”** ，再单击 **“备份”** 。 将出现 **“备份数据库”** 对话框。  
1. 从下拉列表中选择“数据库”  。 
1. 从“备份类型”下拉列表中，选择“完整”。   
1. 在“备份组件”下，选择“数据库”   。 
1. 在“目标”部分中，使用“备份到”下拉列表选择备份目标。   单击“添加”可添加其他备份对象和/或目标  。 若要删除备份目标，请选择该备份目标并单击 **“删除”** 。 若要查看现有备份目标的内容，请选择该备份目标并单击“内容”。 
1. （可选）查看“介质选项”和“备份选项”页面下的其他可用设置   。 要详细了解各种备份选项，请参阅[常规页](back-up-database-general-page.md)、[介质选项页](back-up-database-media-options-page.md)和[备份选项页](back-up-database-backup-options-page.md)。 



### <a name="additional-information"></a>其他信息
- 创建完整数据库备份后，可创建差异数据库备份；有关详细信息，请参阅 [创建差异数据库备份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)。  
- 还可以选择“仅复制备份”  复选框创建仅复制备份。 *仅复制备份*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]独立于常规备份序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的备份。 有关详细信息，请参阅[仅复制备份 (SQL Server)](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  仅复制备份不可用于**差异**备份类型。  
- 如果要备份到 URL，则可禁用“介质选项”页上的“覆盖介质”选项   。 


## <a name="ssms-examples"></a>SSMS 示例  

对于以下示例，使用以下 Transact-SQL 代码创建测试数据库：

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```

### <a name="a-full-back-up-to-disk-to-default-location"></a>A. 完整备份到默认位置的磁盘
在此示例中，将 `SQLTestDB` 数据库备份到默认备份位置处的磁盘。  从未执行 `SQLTestDB` 的备份。
1.  在“对象资源管理器”  中，连接到一个 SQL Server 数据库引擎实例，然后展开该实例。
2.  展开“数据库”  ，右键单击 `SQLTestDB`，然后指向“任务”  ，再单击“备份...”  。
3.  选择“确定”  。

![执行 SQL 备份](media/quickstart-backup-restore-database/backup-db-ssms.png) 
 

### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.完整备份到非默认位置的磁盘**
在此示例中，将 `SQLTestDB` 数据库备份到位于 `F:\MSSQL\BAK` 的磁盘。  之前已执行 `SQLTestDB` 的备份。
1.  在“对象资源管理器”  中，连接到一个 SQL Server 数据库引擎实例，然后展开该实例。
2.  展开“数据库”  ，右键单击 `Sales`，然后指向“任务”  ，再单击“备份...”  。
3.  在“常规”页的“目标”部分中，从“备份到:”下拉列表中选择“磁盘”。    
4.  选择“删除”，直到所有现有备份文件均已删除  。
5.  选择“添加”，这将打开“选择备份目标”对话框   。
6.  在“文件名”文本框中输入 `F:\MSSQL\BAK\Sales_20160801.bak`。 
7.  选择“确定”  。
8.  选择“确定”  。

![更改 DB 位置](media/create-a-full-database-backup-sql-server/change-db-location.png)

### <a name="c--create-an-encrypted-backup"></a>**C.创建加密备份**
在此示例中，将已加密的 `SQLTestDB` 数据库备份到默认备份位置。  

1.  在“对象资源管理器”  中，连接到一个 SQL Server 数据库引擎实例，然后展开该实例。
1. 打开“新建查询”窗口，然后执行以下命令在 `SQLTestDB` 数据库中创建[数据库主密钥](../../relational-databases/security/encryption/create-a-database-master-key.md)和[证书](../../t-sql/statements/create-certificate-transact-sql.md)    。 

    ```sql
    USE [SQLTestDB]
        
    -- Create the database master key
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    
    
    -- Create the certificate
    CREATE CERTIFICATE MyCertificate   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    EXPIRY_DATE = '20201031';  
    GO  
    ```

1.  在对象资源管理器中，展开“数据库”，右键单击 `SQLTestDB`，然后指向“任务”，再单击“备份...”     。
1.  在“介质选项”页的“覆盖介质”部分中，选择“备份到新介质集并清除所有现有备份集”    。
1.  在“备份选项”页的“加密”部分中，选择“加密备份”复选框。   
1.  从“算法”下拉列表中选择 AES 256  。
1.  从“证书”或“非对称密钥”下拉列表中选择 `MyCertificate`。 
1.  选择“确定”  。

![加密备份](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.备份到 Azure Blob 存储服务**


以下三个示例向 Microsoft Azure Blob 存储服务执行完整的 `Sales` 数据库备份。  存储帐户名称为 `mystorageaccount`。  容器名称为 `myfirstcontainer`。  出于简洁的目的，在此处一次列出前四个步骤，之后所有示例将从 **步骤 5** 开始。

1.  在“对象资源管理器”  中，连接到一个 SQL Server 数据库引擎实例，然后展开该实例。
2.  展开“数据库”  ，右键单击 `Sales`，然后指向“任务”  ，再单击“备份...”  。
3.  在“目标”  部分中的“常规”  页上，从“备份到：”  下拉列表中选择“URL” 
4.  单击“添加”  “选择备份目标”  对话框。

#### <a name="striped-backup-to-url-and-a-sql-server-credential-already-exists"></a>已存在到 URL 的条带备份和 SQL Server 凭据

已经创建具有读取、写入和表权限的存储访问策略。  已使用与存储访问策略相关联的共享访问签名创建 SQL Server 凭据 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` 。  

   5.   从“Azure 存储容器：”  文本框中选择 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`
   6.  在“备份文件”  文本框中输入 `Sales_stripe1of2_20160601.bak`。
   7.  单击“确定”  。
   8.  重复步骤 **4** 和 **5**。
   9.  在“备份文件”  文本框中输入 `Sales_stripe2of2_20160601.bak`。
   10.  单击“确定”  。
   11.   单击“确定”  。

#### <a name="a-shared-access-signature-exists-and-a-sql-server-credential-does-not-exist"></a>存在共享访问签名，但不存在 SQL Server 凭据

  5.    在“Azure 存储容器：”  文本框中输入 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`  
  6.    在“共享访问策略：”  文本框中输入共享访问签名。  
  7.    单击“确定”  。  
  8.    单击“确定”  。


#### <a name="a-shared-access-signature-does-not-exist"></a>共享访问签名不存在

  5.    单击“新建容器”  按钮，将会打开“连接到 Microsoft 订阅”  对话框。   
  6.    完成“连接到 Microsoft 订阅”  对话框，然后单击“确定”  ，返回到“选择备份目标”  对话框。  有关其他信息，请参阅 [连接到 Microsoft Azure 订阅](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)。  
  7.    单击“选择备份目标”  对话框中的“确定”  。  
  8.    单击“确定”  。

  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>创建完整数据库备份  
  
1.  执行 BACKUP DATABASE 语句可以创建完整数据库备份，同时指定：  
  
    -   要备份的数据库的名称。   
    -   写入完整数据库备份的备份设备。    
     完整数据库备份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法如下：  
  
     BACKUP DATABASE *database*  
       TO backup_device  [ **,** ...*n* ]    
     [ WITH with_options  [ **,** ...*o* ] ] ;  
  
    |选项|“说明”|  
    |------------|-----------------|  
    |*database*|要备份的数据库。|  
    |*backup_device* [ **,** ...*n* ]|指定一个列表，它包含 1 至 64 个用于备份操作的备份设备。 您可以指定物理备份设备，也可以指定对应的逻辑备份设备（如果已定义）。 若要指定物理备份设备，请使用 DISK 或 TAPE 选项：<br /><br /> { DISK &#124; TAPE } =  物理\_备份\_设备\_名称 <br /><br /> 有关详细信息，请参阅 [备份设备 (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)。|  
    |WITH with_options  [ **,** ...*o* ]|您也可以指定一个或多个附加选项 *o*。 有关某些基本 WITH 选项的信息，请参阅步骤 2。|  
  
2.  （可选）指定一个或多个 WITH 选项。 下面描述了几个基本 WITH 选项。 有关所有 WITH 选项的详细信息，请参阅 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)。  

基本备份集 WITH 选项：

- { COMPRESSION | NO_COMPRESSION }  ：在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 及更高版本中，指定是否为此备份执行 [备份压缩](../../relational-databases/backup-restore/backup-compression-sql-server.md) ，该设置将替代服务器级默认设置。 
- ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  ：仅在 SQL Server 2014 或更高版本中，指定要使用的加密算法以及要用于保护加密的证书或非对称密钥。
- DESCRIPTION = { '_text_' | @_text\_variable_ }      ：指定说明备份集的自由格式文本。 该字符串最长可达 255 个字符。  
- NAME = { backup_set_name | @_backup\_set\_name\_var_ }   ：指定备份集的名称。 名称最长可达 128 个字符。 如果未指定 NAME，它将为空。 
  
 
默认情况下，BACKUP 将备份追加到现有介质集中，并保留现有备份集。 若要显式指定此设置，请使用 NOINIT 选项。 有关附加到现有备份集的信息，请参阅 [媒体集、媒体簇和备份集 (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  

或者，若要将备份介质格式化，可以使用 FORMAT 选项：  

FORMAT [ ,  MEDIANAME=  { media_name   | @  media\_name\_variable  } ] [ ,  MEDIADESCRIPTION =  { text   | @  text\_variable  } ]  
当您第一次使用介质或者希望覆盖所有现有数据时可以使用 FORMAT 子句。 根据需要，可以为新介质指定介质名称和说明。  

> [!IMPORTANT]  
>  当使用 BACKUP 语句的 FORMAT 子句时要十分小心，因为它会破坏以前存储在备份介质中的所有备份。  
  
##  <a name="TsqlExample"></a> Transact-SQL 示例  
对于以下示例，使用以下 Transact-SQL 代码创建测试数据库：

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
  
#### <a name="a-back-up-to-a-disk-device"></a>**A.备份到磁盘设备**  
 下面的示例通过使用 `SQLTestDB` 创建新的介质集，将整个 `FORMAT` 数据库备份到磁盘。  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
TO DISK = 'Z:\SQLServerBackups\SQLTestDB.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B.备份到磁带设备**  
 下面的示例将完整的 `SQLTestDB` 数据库备份到磁带上，并将该备份追加到以前的备份中。  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C.备份到逻辑磁带设备**  
 下例为某个磁带驱动器创建一个逻辑备份设备， 然后，将完整的 SQLTestDB 数据库备份到该设备上。  
  
```sql  
-- Create a logical backup device,   
-- SQLTestDB_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'SQLTestDB_Bak_Tape', '\\.\tape0'; USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO SQLTestDB_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'SQLTestDB_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
使用 **Backup-SqlDatabase** cmdlet。 若要显式指示这是完整数据库备份，请使用其默认值 **Database**  指定 **-BackupAction**参数。 对于完整数据库备份而言，此参数是可选的。  

## <a name="powershell-examples"></a>PowerShell 示例

### <a name="a--full-local-backup"></a>A.  完整的本地备份 
下面的示例在服务器实例 `MyDB` 的默认备份位置创建数据库 `Computer\Instance`的完整数据库备份。 此示例也可以指定 **-BackupAction Database**。  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
### <a name="b--full-backup-to-microsoft-azure"></a>B.  完整备份到 Microsoft Azure 
下面的示例向 Microsoft Azure Blob 存储服务在 `MyServer` 实例上创建 `Sales` 数据库的完整备份。  已经创建具有读取、写入和表权限的存储访问策略。  已使用与存储访问策略相关联的共享访问签名创建 SQL Server 凭据 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。  PowerShell 命令使用 **BackupFile** 参数指定位置 (URL) 和备份文件名。

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" -Database $database -BackupFile $BackupFile;
```
 
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [备份数据库 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
-   [创建差异数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
-   [在简单恢复模式下还原数据库备份 (Transact-SQL)](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
-   [在完整恢复模式下将数据库还原到故障点 (Transact-SQL)](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
-   [将数据库还原到新位置 (SQL Server)](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
-   [使用维护计划向导](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>另请参阅  
- [SQL Server 备份和还原操作疑难解答](https://support.microsoft.com/kb/224071)
- [备份概述 (SQL Server)](../../relational-databases/backup-restore/backup-overview-sql-server.md)
- [事务日志备份 (SQL Server)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)
- [媒体集、媒体簇和备份集 (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
- [备份数据库（“常规”页）](../../relational-databases/backup-restore/back-up-database-general-page.md)
- [备份数据库（“备份选项”页）](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)
- [差异备份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)
- [完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
