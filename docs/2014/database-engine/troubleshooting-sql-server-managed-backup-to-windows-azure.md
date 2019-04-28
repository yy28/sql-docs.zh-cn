---
title: 故障排除 SQL Server 托管备份到 Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd68f6f8bcb83bfbc980be0809e12141403e4012
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842574"
---
# <a name="troubleshooting-sql-server-managed--backup-to-windows-azure"></a>排除针对 Microsoft Azure 的 SQL Server 托管备份的故障
  本主题说明可以用来对[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]操作期间可能发生的错误进行故障排除的任务和工具。  
  
## <a name="overview"></a>概述  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已内置检查和故障排除，因此，在许多情况下，由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]进程本身处理内部错误。  
  
 这样一种情况的示例是导致中断的日志备份文件的删除链接影响可恢复性-[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]将标识日志链中断和计划的备份，以便立即执行。 但是，我们仍建议您监视运行状态，并解决所有需要手动干预的错误。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用系统存储过程、系统视图和扩展事件来记录事件和错误。 系统视图和存储过程提供[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]配置信息、所安排备份的状态以及由扩展事件捕获的错误。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用扩展事件捕获错误以用于故障排除。 除了记录事件外，SQL Server 智能管理策略还提供运行状态，电子邮件通知作业使用这种状态来提供错误和问题的通知。 有关详细信息请参阅[监视器 SQL Server 托管备份到 Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]还使用在手动备份到 Windows Azure 存储（SQL Server 备份到 URL）时使用的相同日志记录。 有关备份到 URL 的详细信息相关的问题，请参阅中的疑难解答部分[SQL Server 备份到 URL 最佳实践和故障排除](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>常规故障排除步骤  
  
1.  启用电子邮件通知，开始接收有关错误和警告的电子邮件。  
  
     或者，也可定期运行 `smart_admin.fn_get_health_status` 以检查合计的错误和计数。 例如，`number_of_invalid_credential_errors` 是尝试备份但出现凭据无效错误的智能备份的次数。 `Number_of_backup_loops` 和 `number_of_retention_loops` 不是错误；但是，它们指示备份线程和保持线程扫描数据库列表的次数。 通常，当@begin_time和@end_time都未提供该函数显示过去 30 分钟内的信息，则通常应该会看到这两个列的非零值。 如果为零，则表示系统过载，甚至系统未响应。 有关详细信息，请参阅**排除系统问题**本主题后面的部分。  
  
2.  检查扩展事件日志，了解错误详细信息和其他相关事件。  
  
3.  使用日志中的信息解决问题。  如果系统出现问题或错误时，可能需要重新启动服务或 SQL Server 代理。  
  
### <a name="common-causes-of-errors"></a>常见错误原因  
 以下是产生故障的常见错误列表：  
  
1.  **更改 SQL 凭据：** 如果凭据的名称由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]发生更改或删除，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]将无法再进行备份。 该更改应该应用于[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]配置设置。  
  
2.  **对存储访问密钥值的更改：** 如果为 Windows Azure 帐户中，更改存储密钥值，但使用新值，不更新 SQL 凭据[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]时对存储进行身份验证将失败，并且无法备份数据库配置为使用此帐户。  
  
3.  **对 Windows Azure 存储帐户的更改：** 删除或重命名存储帐户没有相应更改 SQL 凭据将导致[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]失败并且没有备份将被移除。 如果删除存储帐户，则务必用有效的存储帐户信息重新配置数据库。 如果重命名了存储帐户或更改了密钥值，请确保这些更改反映在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用的 SQL 凭据中。  
  
4.  **对数据库属性的更改：** 更改恢复模式或更改名称可能导致备份失败。  
  
5.  **对恢复模式的更改：** 如果数据库的恢复模式从完整或大容量日志更改为简单，备份将停止，并通过将跳过该数据库[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 有关详细信息，请参阅[SQL Server 托管备份到 Windows Azure:互操作性和共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>最常见的错误消息和解决方案  
  
1.  **启用或配置时出错[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     错误："无法访问存储 URL...提供有效的 SQL 凭据...":您可能会看到此错误和 SQL 凭据的其他类似错误。  在这种情况下，查看的名称以及 SQL 凭据提供，也存储在 SQL 凭据的存储帐户名称和存储访问密钥的信息并确保它们是最新且有效。  
  
     错误:"...无法配置数据库...因为它是系统数据库":你将看到此错误，如果尝试启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]系统数据库。  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不支持系统数据库备份。  要为系统数据库配置备份，请使用其他 SQL Server 备份计术，如维护计划。  
  
     错误:"...提供保持期...":如果你没有指定保留期的数据库或实例，您在第一次配置这些值时，可能会看到关于保持期的错误。 如果您提供的不是 1 到 30 之间的值，可能也会看到错误。 允许对保持期使用的值为 1 到 30 之间的数字。  
  
2.  **电子邮件通知错误：**  
  
     错误："数据库邮件未启用..."-如果启用电子邮件通知，但不是在实例上配置数据库邮件，则会看到此错误。 您必须在实例上配置数据库邮件，才能接收关于[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]运行状态的通知。 有关如何启用数据库邮件的信息，请参阅[配置数据库邮件](../relational-databases/database-mail/configure-database-mail.md)。 要使用数据库邮件接收通知，您还必须启用 SQL Server 代理。 有关详细信息，请参阅[开始之前](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin)。  
  
     以下是可能看到的与电子邮件通知关联的错误编号的列表：  
  
    -   错误号:45209  
  
    -   错误号:45210  
  
    -   错误号:45211  
  
3.  **连接错误：**  
  
    -   **与 SQL 连接相关的错误：** 连接到 SQL Server 实例的问题时，会发生这些错误。 扩展事件通过管理通道公开这些类型的错误。 以下是两个扩展事件，对于与此类型的连接问题相关的错误，可能看到这些扩展事件：  
  
         FileRetentionAdminXEvent，其 event_type 为 SqlError。 有关此错误的详细信息，请查看该事件的 error_code、error_message 和 stack_trace。 Error_code 是 SqlException 的错误号。  
  
         具有以下消息/消息前缀的 SmartBackupAdminXevent：  
  
         *"配置 SQL Server Managed Backup to Windows Azure 默认设置时发生内部错误实例。错误可能是暂时性。"*  
  
         *"可能正在遇到 SQL Server 的连接问题。正在跳过当前迭代中的数据库。"*  
  
         *"查询日志使用情况信息失败。失败可能是暂时性的。正在跳过当前迭代中的数据库。"*  
  
         *"加载 SSMBackup2WA 代理元数据时遇到了 SQL 异常。失败可能是暂时性的。将重试操作。"*  
  
         *"SSMBackup2WA 遇到了 SQL 异常时..."*  
  
    -   **连接到存储帐户时出错：**  
  
         在 event_type 为 XstoreError 的 FileRetentionAdminXEvent 中报告存储异常。 有关此错误的详细信息，请查看该事件的 error_message 和 stack_trace。  
  
         由于 SQL Server 托管备份使用基础的“备份到 URL”技术，因此与存储连接相关的错误同时适用于两个功能。 有关故障排除步骤的详细信息，请参阅**故障排除部分**的[SQL Server 备份到 URL 最佳实践和故障排除](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)一文。  
  
### <a name="troubleshooting-system-issues"></a>排除系统问题  
 以下是系统（SQL Server、SQL Server 代理）有问题的一些场景及其对[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的影响：  
  
-   **Sqlservr.exe 停止响应或停止工作时[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]正在运行：** 如果 SQL Server 停止工作，SQL 代理将正常关闭，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也将停止，事件将记录 SQL Agent.out 文件中。  
  
     如果 SQL Server 停止响应，则在管理通道中记录事件。  事件日志的一个示例：  
  
     *Sql 错误 (引擎未响应或收到 sqlException:SqlException:*   
     *错误代码、 消息和堆栈跟踪将会显示在管理通道 xevent，以及某些额外信息，例如：*   
    *"可能正在遇到 SQL Server 的连接问题。在当前迭代中跳过数据库"*  
  
-   **SQL 代理停止响应或停止工作时[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]正在运行：**  
  
     如果 SQL 代理停止工作，则[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也会停止，而管理通道中将记录事件。 这与 SQL Server 停止响应时的场景类似。  
  
     如果 SQL 代理停止响应，则[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]将无法继续进行备份操作，而管理通道中将记录事件。 事件日志的一个示例：  
  
     *作业挂起： 请参阅管理通道 xevents*   
    *"进度更新尚未从中的 SQL Server 已收到多个"+ Constants.DBBackupInfoMsgMaxWaitTime +"小时数据库备份。 SSM 云备份将继续等待。"*  
  
 如果已启用电子邮件通知，您将收到通知，其中包括**备份循环数**并**保持循环数**。 如果通知中返回的其中一列的值为零或两列的值都为零，则可能表示系统未响应。  
  
> [!WARNING]  
>  生成报表结果的内部进程，假设引擎诊断日志与 SQL 代理错误日志处于同一位置，默认为在 SQL Server 实例的错误日志所在的文件夹中。 如果引擎诊断日志移到与 SQL 代理错误日志位置不同的位置，系统就找不到智能备份诊断日志，电子邮件通知中的报表也就可能不正确。 例如，可能会看到的值**0**在所有字段中报告包括备份循环数和保持循环数。 在这种情况下，诊断日志已移动到其他位置，这不表示系统不响应，只是系统找不到日志。 首先应确保诊断日志的位置和 SQL 代理错误日志处于同一位置。 若要验证当前诊断日志的位置，可以使用[sys.dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations)。 `path`列返回当前位置的引擎诊断日志。  它应与 SQL 代理错误日志位于同一文件夹中。 使用 `dbo.sp_get_sqlagent_properties` 存储过程可以获取 SQL 代理错误日志路径。  
  
 检查扩展事件日志以了解错误的详细信息。 修复错误或重新启动 SQL Server Agent 以更正该状况。  
  
  
