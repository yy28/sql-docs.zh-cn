---
title: SQL Server 托管备份到 Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b7374cd96dac868ae6d3361ee34e18693c340cff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254319"
---
# <a name="sql-server-managed--backup-to-windows-azure"></a>SQL Server 托管备份到 Windows Azure
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]管理并自动执行将 SQL Server 备份到 Windows Azure Blob 存储服务。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]使用的备份策略基于保持期和数据库中的事务工作负载。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 支持指定保持期的时间点还原。   
可在数据库级别或实例级别启用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]以管理 SQL Server 实例上的所有数据库。 SQL Server 可在本地运行，也可在 Windows Azure 虚拟机等托管环境中运行。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 建议用于 Windows Azure 虚拟机上运行的 SQL Server。  
  
## <a name="benefits-of-automating-sql-server-backup-using-includesssmartbackupincludesss-smartbackup-mdmd"></a>使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]自动化 SQL Server 备份的好处  
  
-   目前，自动备份多个数据库需要制定备份策略、编写自定义代码并安排备份。 通过使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，只需提供保持期设置和存储位置。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 计划、 执行和维护备份。  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]可以在数据库级别配置，或以 SQL Server 实例的默认设置来配置。 自动执行备份，使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]具有以下优点：  
  
    -   通过在实例级别设置默认值，可将这些设置应用于任何此后创建的数据库，从而消除了不备份新数据库和丢失数据的风险。  
  
    -   也可在数据库级别启用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]并设置保持期，从而取代在实例级别设置的默认设置。 这使您可以对特定数据库的可恢复性具有更为精细的控制力。  
  
-   有了[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，您便无须为数据库指定备份类型或备份频率。  指定的保持期，和[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]确定的类型和频率备份的数据库将备份存储在 Windows Azure Blob 存储服务。 有关详细信息组条件的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]用来创建备份策略，请参阅[组件和概念](#Concepts)本主题中的部分。  
  
-   配置为使用加密后，即提高备份数据的安全性。 有关详细信息，请参阅[备份加密](backup-encryption.md)  
  
 有关使用适用于 Windows Azure Blob 存储的好处的更多详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份，请参阅[Windows Azure Blob 存储服务使用 SQL Server 备份和还原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
## <a name="terms-and-definitions"></a>术语和定义  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 SQL Server 的一项功能，该功能自动备份数据库并根据保持期维护这些备份。  
  
 保持期  
 保留期由[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]来确定应将哪些备份文件保留在存储以便将数据库恢复到某个点在指定的时间范围内的时间。  支持的值为 1 到 30 天的范围。  
  
 日志链  
 日志备份的连续序列称为日志链。 日志链从数据库的完整备份开始。  
  
##  <a name="Concepts"></a> 要求、 概念和组件  
  
  
###  <a name="Security"></a> Permissions  
 Transact-SQL 是用于配置和监控[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的主要界面。 一般情况下，若要运行配置存储过程、 **db_backupoperator**拥有数据库角色**ALTER ANY CREDENTIAL**权限，并且`EXECUTE`权限**sp_delete_backuphistory**存储的过程是必需的。  用于查看信息的存储过程和函数通常分别需要针对存储过程的 `Execute` 权限以及针对函数的 `Select` 权限。  
  
###  <a name="Prereqs"></a> 先决条件  
 **先决条件：**  
  
 **Windows Azure 存储服务**由[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]用于存储备份文件。    中的详细信息中所述的概念、 结构和创建 Windows Azure 存储帐户的要求[Introduction to Key Components and Concepts](sql-server-backup-to-url.md#intorkeyconcepts)一部分**SQL Server 备份到 URL**本主题。  
  
 **SQL 凭据**用于存储对 Windows Azure 存储帐户进行身份验证所需的信息。 SQL 凭据对象存储帐户名称和访问密钥信息。 有关详细信息，请参阅[Introduction to Key Components and Concepts](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)主题中**SQL Server 备份到 URL**主题。 有关如何创建 SQL 凭据，以存储 Windows Azure 存储身份验证信息的演练，请参阅[第 2 课： 创建 SQL Server 凭据](../../tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
###  <a name="Concepts_Components"></a> 概念和关键组件  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]是一项管理备份操作的功能。 它将存储中的元数据**msdb**数据库，并使用系统作业写入完整数据库备份和事务日志备份。  
  
#### <a name="components"></a>组件  
 Transact-SQL 是与 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]交互的主要界面。 系统存储过程用于启用、配置和监视 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 系统函数用于检索现有配置设置、参数值和备份文件信息。 扩展事件用于呈现错误和警告。 警报机制通过 SQL 代理作业和 SQL Server 基于策略的管理启用。 以下列表列出了与 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相关的对象及其功能的说明。  
  
 也有 PowerShell cmdlet 可用于配置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 SQL Server Management Studio 支持还原由 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 使用 **“还原数据库”** 任务创建的备份  
  
|||  
|-|-|  
|系统对象|Description|  
|**MSDB**|存储由 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]创建的所有备份的元数据和备份历史记录。|  
|[smart_admin.set_db_backup &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/en-us/library/dn451013(v=sql.120).aspx)|为数据库启用和配置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的系统存储过程。|  
|[smart_admin.set_instance_backup &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|系统存储过程启用和配置默认设置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]SQL Server 实例。|  
|[smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|用于暂停和继续运行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的系统存储过程。|  
|[smart_admin.sp_set_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|用于为[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]启用和配置监视的系统存储过程。 示例：启用扩展事件、通知的邮件设置。|  
|[smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|系统存储过程用于启用要使用的数据库执行即席备份[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]而不会中断日志链。|  
|[smart_admin.fn_backup_db_config &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|返回当前的系统函数[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]数据库，或在实例上的所有数据库的状态和配置值。|  
|[smart_admin.fn_is_master_switch_on &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|返回主开关状态的系统函数。|  
|[smart_admin.sp_get_backup_diagnostics &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|用于返回扩展事件所记录的事件的系统存储过程。|  
|[smart_admin.fn_get_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|返回备份系统设置当前值（如监视和警报的电子邮件设置）的系统函数。|  
|[smart_admin.fn_available_backups &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|用于检查指定数据库或实例所有数据库的可用备份的存储过程。|  
|[smart_admin.fn_get_current_xevent_settings &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|返回当前扩展事件设置的系统函数。|  
|[smart_admin.fn_get_health_status &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|返回由指定期间扩展事件记录的合计错误数的系统函数。|  
|[监视针对 Microsoft Azure 的 SQL Server 托管备份](sql-server-managed-backup-to-microsoft-azure.md)|多种扩展事件，涉及监视[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、通过电子邮件通知错误和警告、进行 SQL Server 基于策略的管理。|  
  
#### <a name="backup-strategy"></a>备份策略  
 **使用的备份策略[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  
  
 安排的备份类型和备份频率是根据数据库的工作负载确定的。 保持期设置用于决定应在存储中保留备份文件的时间长度以及能否将数据库恢复到保留期内的某个时间点。  
  
 **备份容器和文件命名约定：**  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]使用 SQL Server 实例名称命名所有数据库（可用性数据库除外）的 Windows Azure 存储容器。  而使用可用性组 GUID 命名可用性数据库的 Windows Azure 存储容器。  
  
 按照以下约定命名非可用性数据库的备份文件：使用数据库名称的前 40 个字符、不含“-”的数据库 GUID 以及时间戳创建名称。 在各段之间插入下划线字符作为分隔符。 完整备份使用 **.bak** 文件扩展名，日志备份使用 **.log** 。 对于可用性组数据库，除了上方所述的文件命名约定之外，还在 40 个字符的数据库名称后添加可用性组数据库 GUID。 可用性组数据库 GUID 值为 sys.databases 中 group_database_id 的值。  
  
 **完整数据库备份：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]代理安排完整数据库备份，如果以下为真。  
  
-   初次为数据库启动 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，或在实例级使用默认设置启用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 时。  
  
-   自上次完备数据库备份以来的日志增长等于或超过 1 GB。  
  
-   距上次完整数据库备份以来已超过一周的最大时间间隔。  
  
-   日志链中断。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 会定期进行检查，通过比较备份文件的第一个和最后一个 LSN 确定日志链是否完整。 如果日志链因为任何原因而存在中断，则 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 会安排一次完整数据库备份。 日志链断裂的最常见原因可能是使用 Transact-SQL 或通过 SQL Server Management Studio 中的备份任务发出了备份命令。  其他常见的情况包括意外删除了备份文件或意外的备份覆盖。  
  
 **事务日志备份：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]安排一次日志备份，如果任意下列条件成立：  
  
-   找不到日志备份历史记录。 在首次启动 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 时通常存在这种情况。  
  
-   使用的事务日志空间为 5 MB 或更大。  
  
-   距上次日志备份达到 2 小时的最大时间间隔。  
  
-   事务日志备份滞后于完整备份数据库时。 目标是使日志链保持在完整备份之前。  
  
#### <a name="retention-period-settings"></a>保持期设置  
 在启用备份时，必须以天为单位设置保持期：最短为 1 天，最长为 30 天。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 根据保持期设置评估能否恢复到指定的时间点，以决定要保留什么备份文件并找出要删除的备份文件。 备份的 backup_finish_date 用于确定和匹配由保持期设置指定的时间。  
  
#### <a name="important-considerations"></a>重要注意事项  
 有一些注意事项对于理解[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]操作十分重要。 下面列出了这些注意事项：  
  
-   对于数据库，如果现有完整数据库备份作业正在运行，则 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 将等待当前作业完毕，然后对该数据库进行另一次完整数据库备份。 同样，给定时间只能运行一个事务日志备份。 但是，完整数据库备份和事务日志备份可以同时运行。 失败会记录为扩展事件。  
  
-   如果安排了超过 10 个并发的完整数据库备份，则会通过扩展事件的调试渠道发出一个警告。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 随后针对其余需要备份的数据库保留一个优先级队列，直到安排并完成所有备份。  
  
###  <a name="support_limits"></a> 支持限制  
 以下是对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的一些特定限制：  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]代理只支持数据库完整备份和日志备份。  不支持文件备份自动化。  
  
-   当前支持使用 Transact-SQL 进行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]操作。 可通过使用扩展事件来进行监视和故障排除。 仅在配置 SQL Server 实例的存储和保持期默认设置以及根据 SQL Server 基于策略的管理策略监视备份状态和整体运行状况时支持 PowerShell 和 SMO。  
  
-   不支持系统数据库。  
  
-   Windows Azure Blob 存储服务是唯一支持的备份存储选项。 不支持备份到磁盘或磁带。  
  
-   当前，Windows Azure 存储中的页 Blob 允许文件大小最大为 1 TB。 备份大于 1 TB 的文件将失败。 为了避免出现这种情况，建议对于大型数据库使用压缩，并在设置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前测试备份文件大小。 可通过备份到本地磁盘或使用 `BACKUP TO URL` Transact-SQL 语句手动备份到 Windows Azure 进行测试。 有关详细信息，请参阅 [SQL Server Backup to URL](sql-server-backup-to-url.md)。  
  
-   恢复模式：只支持设置为完整或大容量日志模式的数据库。  不支持设置为简单恢复模式的数据库。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 可能有一些限制。 有关详细信息，请参阅[SQL Server 托管备份到 Windows Azure： 互操作性和共存](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
|||  
|-|-|  
|**任务说明**|**主题**|  
|基本任务包括：为数据库配置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]或在实例级别配置默认设置，在实例或数据库级别禁用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，暂停和重新启动[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|[针对 Microsoft Azure 的 SQL Server 托管备份 - 保留和存储设置](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**教程：** 配置和监控的分步说明[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|[针对 Microsoft Azure 设置 SQL Server 托管备份](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**教程：** 配置和监控的分步说明[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]可用性组中的数据库。|[为可用性组设置针对 Microsoft Azure 的 SQL Server 托管备份](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|与监视[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相关的工具、概念和任务。|[监视针对 Microsoft Azure 的 SQL Server 托管备份](sql-server-managed-backup-to-microsoft-azure.md)|  
|对[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]进行故障排除的工具和步骤。|[排除针对 Microsoft Azure 的 SQL Server 托管备份的故障](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>请参阅  
 [Windows Azure Blob 存储服务使用 SQL Server 备份和还原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server 备份到 URL](sql-server-backup-to-url.md)   
 [SQL Server 托管备份到 Windows Azure： 互操作性和共存](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [排除针对 Microsoft Azure 的 SQL Server 托管备份的故障](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
