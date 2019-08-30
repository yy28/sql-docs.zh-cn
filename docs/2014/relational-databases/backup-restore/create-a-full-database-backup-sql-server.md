---
title: 创建完整数据库备份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: ec94f8387d7b833a80cd4df09f7d4208974d40a7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154823"
---
# <a name="create-a-full-database-backup-sql-server"></a>创建完整数据库备份 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建完整数据库备份。  
  
> [!NOTE]  
>  有关 SQL Server 备份到 Azure Blob 存储服务的信息, 请参阅[SQL Server 通过 Azure Blob 存储服务进行备份和还原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要创建完整数据库备份, 请使用:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   不允许在显式或隐式事务中使用 BACKUP 语句。  
  
-   无法在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中还原较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建的备份。  
  
-   有关详细信息，请参阅 [备份概述 (SQL Server)](backup-overview-sql-server.md)。  
  
###  <a name="Recommendations"></a> 建议  
  
-   随着数据库不断增大，完整备份需花费更多时间才能完成，并且需要更多的存储空间。 因此，对于大型数据库而言，您可以用一系列“差异数据库备份”来补充完整数据库备份。 有关详细信息，请参阅 [差异备份 (SQL Server)](differential-backups-sql-server.md)。  
  
-   你可以使用 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 系统存储过程估计完整数据库备份的大小。  
  
-   默认情况下，每个成功的备份操作都会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和系统事件日志中添加一个条目。 如果非常频繁地备份日志，这些成功消息会迅速累积，从而产生一个巨大的错误日志，这样会使查找其他消息变得非常困难。 在这些情况下，如果任何脚本均不依赖于这些日志条目，则可以使用跟踪标志 3226 取消这些条目。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)。  
  
###  <a name="Security"></a> 安全性  
 针对数据库备份，TRUSTWORTHY 设置为 OFF。 有关如何将 TRUSTWORTHY 设置为 ON 的详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，`PASSWORD` 和 `MEDIAPASSWORD` 选项不可再用于创建备份； 不过，您仍可以还原使用密码创建的备份。  
  
####  <a name="Permissions"></a> Permissions  
 默认情况下，为 **sysadmin** 固定服务器角色以及 **db_owner** 和 **db_backupoperator** 固定数据库角色的成员授予 BACKUP DATABASE 和 BACKUP LOG 权限。  
  
 备份设备的物理文件的所有权和权限问题可能会妨碍备份操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须能够读取和写入设备；运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户必须具有写入权限。 但是，用于在系统表中为备份设备添加项目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)不检查文件访问权限。 备份设备物理文件的这些问题可能直到为备份或还原而访问物理资源时才会出现。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定备份任务时，可以通过单击“脚本”按钮并选择脚本目标生成相应的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 脚本。  
  
#### <a name="to-back-up-a-database"></a>备份数据库  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”** ，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击数据库，指向 **“任务”** ，再单击 **“备份”** 。 将出现 **“备份数据库”** 对话框。  
  
4.  `Database`在列表框中, 验证数据库名称。 您也可以从列表中选择其他数据库。  
  
5.  可以对任意恢复模式（**FULL**、**BULK_LOGGED** 或 **SIMPLE**）执行数据库备份。  
  
6.  在 **“备份类型”** 列表框中，选择 **“完整”** 。  
  
     请注意，创建了完整数据库备份后，可以创建差异数据库备份；有关详细信息，请参阅 [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)。  
  
7.  还可以根据需要选择“仅复制备份”创建仅复制备份。 *仅复制备份*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]独立于常规备份序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的备份。 有关详细信息，请参阅[仅复制备份 (SQL Server)](copy-only-backups-sql-server.md)。  
  
    > [!NOTE]  
    >  选择“差异”选项时，无法创建仅复制备份。  
  
8.  对于 "**备份组件**" `Database`, 单击。  
  
9. 可以接受 **“名称”** 文本框中建议的默认备份集名称，也可以为备份集输入其他名称。  
  
10. 或者，在 **“说明”** 文本框中，输入备份集的说明。  
  
11. 通过单击 **“磁盘”** 、 **“类型”** 或 **“URL”** ，选择备份目标的类型。 若要选择包含单个介质集的多个磁盘或磁带机（最多为 64 个）的路径，请单击 **“添加”** 。 选择的路径将显示在 **“备份到”** 列表框中。  
  
     若要删除备份目标，请选择该备份目标并单击 **“删除”** 。 若要查看备份目标的内容，请选择该备份目标并单击 **“内容”** 。  
  
12. 若要查看或选择介质选项，请在 **“选择页”** 窗格中单击 **“介质选项”** 。  
  
13. 可以通过单击以下选项之一来选择 **“覆盖介质”** 选项：  
  
    -   **备份到现有介质集**  
  
         对于此选项，请单击 **“追加到现有备份集”** 或 **“覆盖所有现有备份集”** 。 有关详细信息，请参阅 [媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         或者选择 **“检查介质集名称和备份集过期时间”** ，以使备份操作对介质集和备份集的过期日期和时间进行验证。  
  
         或者在 **“介质集名称”** 文本框中输入名称。 如果没有指定名称，将使用空白名称创建介质集。 如果指定了介质集名称，将检查介质（磁带或磁盘），以确定实际名称是否与此处输入的名称匹配。  
  
        > [!IMPORTANT]  
        >  如果在 **“常规”** 页中选择了 **“URL”** 作为备份目标，则禁用此选项。 有关详细信息，请参阅[备份数据库（媒体选项页）](back-up-database-media-options-page.md)。  
        >   
        >  如果要使用加密，则请勿选择此选项。 如果选择此选项，则将禁用 **“备份选项”** 页中的加密选项。 追加到现有备份集时不支持加密。  
  
    -   **备份到新介质集并清除所有现有备份集**  
  
         对于该选项，请在 **“新建介质集名称”** 文本框中输入名称，并在 **“新建介质集说明”** 文本框中描述介质集（可选）。  
  
        > [!IMPORTANT]  
        >  如果在 **“常规”** 页中选择了 **“URL”** ，则禁用此选项。 备份到 Azure 存储时不支持这些操作。  
  
14. 在 **“可靠性”** 部分中，根据需要选中以下任意选项：  
  
    -   **完成后验证备份**。  
  
    -   **“写入介质前检查校验和”** 和 **“出现校验和错误时继续”** （可选）。 有关校验和的信息，请参阅[在备份和还原期间可能的媒体错误 (SQL Server)](possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
15. 如果备份到磁带驱动器（如同“常规”页的“目标”部分指定的一样），则“备份后卸载磁带”选项处于活动状态。 单击此选项可以激活 **“卸载前倒带”** 选项。  
  
    > [!NOTE]  
    >  除非备份的是事务日志（如同“常规”页的“备份类型”部分中指定的一样），否则“事务日志”部分中的选项处于不活动状态。  
  
16. 若要查看或选择备份选项，请在 **“选择页”** 窗格中单击 **“备份选项”** 。  
  
17. 指定备份集何时过期以及何时可以覆盖备份集而不用显式跳过过期数据验证：  
  
    -   若要使备份集在特定天数后过期，请单击 **“之后”** （默认选项），并输入备份集从创建到过期所需的天数。 此值范围为 0 到 99999 天；0 天表示备份集将永不过期。  
  
         默认值在“服务器属性”对话框（位于“数据库设置”页上）的“默认备份媒体保持期（天）”选项中设置。 若要访问它，请在对象资源管理器中右键单击服务器名称，选择属性，再选择“数据库设置”页。  
  
    -   若要使备份集在特定日期过期，请单击 **“在”** ，并输入备份集的过期日期。  
  
         有关备份过期日期的详细信息，请参阅 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)。  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 及更高版本支持 [备份压缩](backup-compression-sql-server.md)。 默认情况下，是否压缩备份取决于 **backup-compression default** 服务器配置选项的值。 但是，不管当前服务器级默认设置如何，都可以通过选中 **“压缩备份”** 来压缩备份，并且可以通过选中 **“不压缩备份”** 来防止压缩备份。  
  
     **查看或更改当前备份压缩默认值**  
  
    -   [查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. 指定是否要对备份使用加密。 选择要用于加密步骤的加密算法，然后从现有证书或非对称密钥的列表中提供一个证书或非对称密钥。 SQL Server 2014 或更高版本中支持加密。 有关加密选项的详细信息，请参阅[备份数据库（备份选项页）](back-up-database-backup-options-page.md)。  
  
> [!NOTE]  
>  此外，还可以使用维护计划向导来创建数据库备份。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-full-database-backup"></a>创建完整数据库备份  
  
1.  执行 BACKUP DATABASE 语句可以创建完整数据库备份，同时指定：  
  
    -   要备份的数据库的名称。  
  
    -   写入完整数据库备份的备份设备。  
  
     完整数据库备份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法如下：  
  
     BACKUP DATABASE *database*  
  
     TO backup_device [ **,** ...*n* ]  
  
     [ WITH with_options [ **,** ...*o* ] ] ;  
  
    |选项|“说明”|  
    |------------|-----------------|  
    |*database*|要备份的数据库。|  
    |*backup_device* [ **,** ...*n* ]|指定一个列表，它包含 1 至 64 个用于备份操作的备份设备。 您可以指定物理备份设备，也可以指定对应的逻辑备份设备（如果已定义）。 若要指定物理备份设备，请使用 DISK 或 TAPE 选项：<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> 有关详细信息，请参阅 [备份设备 (SQL Server)](backup-devices-sql-server.md)。|  
    |WITH with_options [ **,** ...*o* ]|您也可以指定一个或多个附加选项 *o*。 有关某些基本 WITH 选项的信息，请参阅步骤 2。|  
  
2.  （可选）指定一个或多个 WITH 选项。 下面描述了几个基本 WITH 选项。 有关所有 WITH 选项的详细信息，请参阅 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)。  
  
    -   基本备份集 WITH 选项：  
  
         { COMPRESSION | NO_COMPRESSION }  
         在 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 及更高版本中，指定是否为此备份执行 [备份压缩](backup-compression-sql-server.md) ，该设置将替代服务器级默认设置。  
  
         ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  
         仅在 SQL Server 2014 或更高版本中，指定要使用的加密算法以及要用于保护加密的证书或非对称密钥。  
  
         说明 **=** { **" *`text`* '** text_variable | } " **@**  
         指定说明备份集的自由格式文本。 该字符串最长可达 255 个字符。  
  
         NAME **=** { *backup_set_name* |  **@** _backup_set_name_var_ }  
         指定备份集的名称。 名称最长可达 128 个字符。 如果未指定 NAME，它将为空。  
  
    -   基本备份集 WITH 选项：  
  
         默认情况下，BACKUP 将备份追加到现有介质集中，并保留现有备份集。 若要显式指定此设置，请使用 NOINIT 选项。 有关附加到现有备份集的信息，请参阅 [媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         或者，若要将备份介质格式化，可以使用 FORMAT 选项：  
  
         FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media_name_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text_variable_ } ]  
         当您第一次使用介质或者希望覆盖所有现有数据时可以使用 FORMAT 子句。 根据需要，可以为新介质指定介质名称和说明。  
  
        > [!IMPORTANT]  
        >  当使用 BACKUP 语句的 FORMAT 子句时要十分小心，因为它会破坏以前存储在备份介质中的所有备份。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. 备份到磁盘设备  
 下面的示例通过使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 创建新的介质集，将整个 `FORMAT` 数据库备份到磁盘。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>B. 备份到磁带设备  
 下面的示例将完整的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库备份到磁带上，并将该备份追加到以前的备份中。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. 备份到逻辑磁带设备  
 下例为某个磁带驱动器创建一个逻辑备份设备， 然后将完整的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库备份到该设备上。  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
1.  使用 `Backup-SqlDatabase` cmdlet。 若要显式指示这是完整数据库备份, 请指定 **-BackupAction**参数及其默认值`Database`。 对于完整数据库备份而言，此参数是可选的。  
  
     下面的示例在服务器实例 `MyDB` 的默认备份位置创建数据库 `Computer\Instance`的完整数据库备份。 此示例也可以指定 `-BackupAction Database`。  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [备份数据库 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
-   [还原数据库备份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [在简单恢复模式下还原数据库备份 (Transact-SQL)](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [在完整恢复模式下将数据库还原到故障点 (Transact-SQL)](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [将数据库还原到新位置 (SQL Server)](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [使用维护计划向导](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>请参阅  
 [备份概述 (SQL Server)](backup-overview-sql-server.md)   
 [事务日志备份 (SQL Server)](transaction-log-backups-sql-server.md)   
 [媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [备份数据库（“常规”页）](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [备份数据库（“备份选项”页）](back-up-database-backup-options-page.md)   
 [差异备份 (SQL Server)](differential-backups-sql-server.md)   
 [完整数据库备份 (SQL Server)](full-database-backups-sql-server.md)  
  
  
