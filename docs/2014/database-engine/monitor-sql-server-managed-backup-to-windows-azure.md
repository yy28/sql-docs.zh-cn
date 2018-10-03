---
title: 监视 SQL Server 托管备份到 Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3406468961dcd5817fb88b5a30098177ec6ac67
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073237"
---
# <a name="monitor-sql-server-managed-backup-to-windows-azure"></a>监视 SQL Server 托管备份到 Windows Azure
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]内置多种措施，可在备份过程中找出问题和错误，如有可能，再通过纠正措施纠正这些问题。  但是，有一些需要用户干预的情况。 本主题介绍可用于确定备份的整体运行状况和标识需解决的任何错误的工具。  
  
## <a name="overview-of-includesssmartbackupincludesss-smartbackup-mdmd-built-in-debugging"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的内置调试概述  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]定期检查计划的备份并尝试重新安排任何失败的备份。 它定期轮询存储帐户以找出日志链中影响数据库可恢复性的中断情况，并且相应地安排新备份。 它还会考虑 Windows Azure 限制策略，并且具有管理多个数据库备份的机制。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用扩展事件跟踪所有活动。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]代理使用的扩展事件通道包括管理、操作、分析和调试。 属于管理类别的事件通常与错误相关且要求用户干预，并且默认情况下是启用的。 分析事件默认情况下也启用，但通常与要求用户干预的错误无关。 操作事件通常是信息性的。 例如，操作事件包含计划备份、备份的成功完成等。调试最详细，并且[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在内部用来确定问题和纠正措施（如果需要）。  
  
### <a name="configure-monitoring-parameters-for-includesssmartbackupincludesss-smartbackup-mdmd"></a>为[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]配置监视参数  
 **Smart_admin.sp_set_parameter**系统存储过程，可指定监视设置。 以下部分演练启用扩展事件以及针对错误和警告启用电子邮件通知的过程。  
  
 **Smart_admin.fn_get_parameter**函数可用于获取特定参数或所有已配置的参数的当前设置。 如果从未配置参数，则此函数不返回任何值。  
  
1.  连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 这将返回扩展事件的当前配置和电子邮件通知。  
  
```  
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 有关详细信息，请参阅[smart_admin.fn_get_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)  
  
### <a name="extended-events-for-monitoring"></a>用于监视的扩展事件  
 默认情况下，启用管理、操作和分析事件。 管理事件最严重，在找出需要手动干预才能解决问题的错误时很有用。 可能要开启操作和调试事件，但要考虑到这些事件为详细事件，可能需要进行一些筛选。 以下过程描述如何监视通过扩展事件记录的事件。  
  
> [!IMPORTANT]  
>  与 SQL 引擎的扩展事件不同，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不支持扩展事件会话概念。 系统存储过程和函数是用于与扩展事件交互的工具。 您还可以从日志目录查看扩展事件日志。  
  
##### <a name="to-configure-and-view-extended-events"></a>配置和查看扩展事件  
  
1.  通过运行以下查询查看可用的扩展事件通道及其当前状态：  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     此查询的输出将显示 event_name，无论它是否可配置以及当前是否启用。  有关详细信息，请参阅[smart_admin.fn_get_current_xevent_settings &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)。  
  
2.  若要启用调试事件，请运行以下查询：  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
     有关该存储过程的详细信息，请参阅[smart_admin.sp_set_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)。  
  
3.  若要查看记入日志的事件，请使用以下查询：  
  
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
  
### <a name="aggregated-error-countshealth-status"></a>聚合的错误计数/运行状态  
 **Smart_admin.fn_get_health_status**函数将返回一个可用于监视运行状况状态的每个类别的聚合的错误计数表[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 本主题中后面介绍的系统配置的电子邮件通知机制也使用这个相同的函数。   
这些聚合的计数可用于监视系统运行状况。 例如，如果 number_ of_retention_loops 列在 30 分钟内为 0，则可能保持管理占用较长时间，或者甚至未正确工作。 非零错误列可能指示问题，并且应查看扩展事件日志以便发现问题。 或者，调用**smart_admin.sp_get_backup_diagnostics**存储过程以查找错误的详细信息。  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>使用代理通知以便评估备份状态和运行状况  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]包括一个通知机制，后者基于 SQL Server 基于策略的管理策略。  
  
 **先决条件：**  
  
-   使用此功能需要数据库邮件。 有关如何启用数据库邮件的 SQL Server 实例的详细信息，请参阅[配置数据库邮件](../relational-databases/database-mail/configure-database-mail.md)。  
  
-   SQL Server 代理警报系统属性应设置为使用数据库邮件。  
  
 **通知体系结构：**  
  
-   **基于策略的管理：** 设置了两个策略来监视备份运行状况：**智能管理系统运行状况策略**，和**智能管理用户操作运行状况策略**。 智能管理系统运行状况策略评估严重错误（例如 SQL 凭据无效或缺少 SQL 凭据、连接错误），并且报告系统的运行状况。 这些问题通常要求手动操作以便纠正基本问题。 智能管理用户操作运行状况策略评估警告，例如损坏的备份等。  这些问题可能无需任何操作，只是对某一事件的警告。 此类问题应该由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]代理自动负责处理。  
  
-   **SQL Server 代理**作业： 使用包含三个作业步骤的 SQL Server 代理作业执行通知。 在第一个作业步骤中，它将进行检测以便查看[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]是为数据库还是实例配置的。 如果它发现启用并配置了[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，则它执行第二步：执行一个 PowerShell cmdlet，后者通过评估 SQL Server 基于策略的管理策略，评估运行状况。 如果它发现错误或警告，则它将失败，而这将触发第三步：第三步发出一个电子邮件通知，其中含有错误/警告报表。  但是，默认情况下不启用此 SQL Server 代理作业。 若要启用电子邮件通知作业，请使用**smart_admin.sp_set_backup_parameter**系统存储过程。  下面的过程更详细地说明了这些步骤：  
  
##### <a name="enabling-email-notification"></a>启用通知电子邮件  
  
1.  如果尚未配置数据库邮件，使用中所述的步骤[配置数据库邮件](../relational-databases/database-mail/configure-database-mail.md)。  
  
2.  将数据库设置为用于 SQL Server 警报系统的邮件系统： 右键单击**SQL Server 代理**，选择**警报系统**，检查**启用邮件配置文件**框中，选择**数据库邮件**作为**邮件系统**，然后选择以前创建的邮件配置文件。  
  
3.  在查询窗口中运行以下查询并提供要将通知发送到的电子邮件地址：  
  
    ```  
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
    ```  
  
     这将创建一个 SQL Server 代理作业，它用于收集运行状态并且在没有与备份有关的错误或问题时发送通知。  
  
 下面是一个示例脚本，它通过 SQL Server 代理作业启用数据库邮件和设置电子邮件通知  
  
```  
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification  
  
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>使用 PowerShell 设置自定义运行状况监视  
 **Test-sqlsmartadmin** cmdlet 可用于创建自定义运行状况监视。 例如，可在实例级别配置前一部分中所述的通知选项。  如果将若干 SQL Server 实例配置为使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，则可使用 PowerShell cmdlet 创建脚本，为所有实例收集备份的状态和运行状况。  
  
 **Test-sqlsmartadmin** cmdlet 评估的错误和警告返回由 SQL Server 基于策略的管理策略，并且报告汇总状态。  默认情况下，此 cmdlet 使用系统策略。 若要包括任何自定义策略，请使用 `–AllowUserPolicies` 参数。  
  
 下面是一个示例 PowerShell 脚本，它基于系统策略以及任何创建的用户策略返回错误和警告的报告：  
  
```  
$policyResults = get-sqlsmartadmin | test-sqlsmartadmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | select Name, Category, Expression, Result, Exception | fl  
  
```  
  
 下面的脚本返回默认实例的报告和警告的详细报告：  
  
```  
PS C:\>PS SQLSERVER:\SQL\COMPUTER\DEFAULT> (get-sqlsmartadmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>MSDB 数据库中的对象  
 为实现功能，安装了一些对象。 这些对象仅供内部使用。 但是，有一个系统表对于监视备份状态可能很有用：smart_backup_files。 大部分信息存储在此表与监视类似于备份，数据库的类型名称、 第一个和最后一个 lsn、 备份到期日期通过系统函数公开[smart_admin.fn_available_backups &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql). 但是，使用该函数时无法使用 smart_backup_files 表中指示备份文件状态的 status 列。 下面是一个示例查询，可使用它从系统表检索某些信息（包括状态）：  
  
```  
USE msdb  
GO  
SELECT  
 database_name AS [Database Name]  
,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;  
  
```  
  
 以下详细介绍返回的不同状态：  
  
-   **Available-a:** 这是正常的备份文件。 备份已完成，并已确认 Windows Azure 存储中有该备份可用。  
  
-   **正在复制 – b:** 此状态是专门为可用性组数据库。 如果 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 检测到备份日志链中断，则它将首先尝试找出可能导致备份链中断的备份。 在查找备份文件时，它尝试将文件复制到 Windows Azure 存储。 在进行复制过程时，它将显示此状态。  
  
-   **Copy Failed-f:** 类似于 Copy In Progress，这是专门用于可用性组数据库。 如果复制过程失败，则将状态标为 F。  
  
-   **Corrupted-c:** 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]是无法通过多个尝试后执行 RESTORE HEADER_ONLY 命令验证备份文件存储中的，会将标记此文件为已损坏。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 将安排一次备份以确保损坏的文件不会导致备份链中断。  
  
-   **Deleted-d:** Windows Azure 存储中找不到相应的文件。 如果删除的文件导致备份链中断，则 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 将安排一次备份。  
  
-   **Unknown-u:** 此状态指示[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]尚未能够验证文件是否存在以及 Windows Azure 存储中的其属性。 下次运行此过程时（大约每 15 分钟一次），将更新此状态。  
  
  
