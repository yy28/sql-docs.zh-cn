---
title: 将日志传送升级到 SQL Server 2014 （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 773426ed91039ee4c0c6fd224547e44102f9846b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175412"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>将日志传送升级到 SQL Server 2014 (Transact-SQL)
  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时，有可能保留日志传送配置。 本主题介绍升级日志传送配置的备用方案和最佳做法。

> [!NOTE]
>  [中引入了](../../relational-databases/backup-restore/backup-compression-sql-server.md) 备份压缩 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]。 升级后的日志传送配置使用“备份压缩默认值”  服务器级配置选项控制是否对事务日志备份文件使用备份压缩。 可以为每个日志传送配置指定日志备份的备份压缩行为。 有关详细信息，请参阅[配置日志传送 (SQL Server)](configure-log-shipping-sql-server.md)。


##  <a name="protect-your-data-before-the-upgrade"></a><a name="ProtectData"></a>升级之前保护数据
 建议您最好在日志传送升级之前保护好您的数据。

 **保护数据**

1.  对各个主数据库执行完整数据库备份。

     有关详细信息，请参阅 [创建完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)中创建差异数据库备份。

2.  对各个主数据库运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。

##  <a name="upgrading-the-monitor-server-instance"></a><a name="UpgradeMonitor"></a>升级监视服务器实例
 监视服务器实例（如果存在）可随时升级。

 升级监视服务器时，日志传送配置仍将有效，但其状态不会记录在监视器上的表中。 监视服务器正在升级期间，已配置的任何警报都不会触发。 升级完毕后，可以通过执行 [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql) 系统存储过程来更新监视器表中的信息。

##  <a name="upgrading-log-shipping-configurations-with-a-single-secondary-server"></a><a name="UpgradeSingleSecondary"></a>使用单个辅助服务器升级日志传送配置
 本节讲述的升级过程适用于由主服务器和唯一一个辅助服务器组成的配置。 下图显示了此配置，其中 A 为主服务器实例，B 为单一辅助服务器实例。

 ![一台辅助服务器，无监视服务器](../media/ls-2-wayconfig-nomonitor.gif "一台辅助服务器，无监视服务器")

 有关升级多个辅助服务器的信息，请参阅本主题后面的 [升级多个辅助服务器实例](#MultipleSecondaries)。
 

###  <a name="upgrading-the-secondary-server-instance"></a><a name="UpgradeSecondary"></a>升级辅助服务器实例
 升级主服务器实例之前的升级过程包括将辅助服务器实例的日志传送配置从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。 辅助服务器实例必须总是先于主服务器实例升级。 由于在较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建的备份无法在较旧版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中还原，所以如果主服务器先于辅助服务器升级，将导致日志传送失败。

 由于升级后的辅助服务器继续还原 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本主服务器的日志备份，因此日志传送在整个升级过程中都不间断。 升级辅助服务器实例的过程部分取决于日志传送配置是否具有多个辅助服务器。 有关详细信息，请参阅本主题后面的 [升级多个辅助服务器实例](#MultipleSecondaries)。

 辅助服务器实例正在升级期间，日志传送复制和还原作业不运行，因此未还原的事务日志备份将累积。 累积的数量取决于主服务器上进行计划备份的频率。 此外，如果还配置了单独的监视服务器，则若未执行还原的时间超过了所配置的时间间隔，就会引发警报。

 辅助服务器升级完毕后，日志传送代理作业即开始继续复制和还原主服务器实例（服务器 A）的日志备份。辅助服务器使辅助数据库达到最新所需的时间会有所不同，具体情况取决于升级辅助服务器占用的时间和主服务器上进行备份的频率。

> [!NOTE]
>  服务器升级期间，辅助数据库不会升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 数据库。 只有联机时它才会升级。

> [!IMPORTANT]
>  对于要求升级的数据库，不支持 RESTORE WITH STANDBY 选项。 如果已使用 RESTORE WITH STANDBY 配置了升级的辅助数据库，则在升级后可能不再能够还原事务日志。 要对该辅助数据库恢复日志传送，您需要再次对该备用服务器设置日志传送。 有关 "备用" 选项的详细信息，请参阅[RESTORE Arguments &#40;transact-sql&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)。

###  <a name="upgrading-the-primary-server-instance"></a><a name="UpgradePrimary"></a> 升级主服务器实例
 计划升级时，需要考虑的一个重要事项是数据库将处于不可用状态的时间。 最简单的升级方案（下文的方案 1）将使得数据库在主服务器升级期间不可用。

 如果能在升级原始主服务器之前，将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本主服务器故障转移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 辅助服务器（下文的方案 2），则可以最大限度地提高数据库的可用性，但这样做会加大升级过程的复杂程度。 故障转移方案有两种不同的形式。 一种是切换回原始主服务器并保持原始日志传送配置。 另一种是在升级原始主服务器之前删除原始日志传送配置，随后使用新的主服务器创建新配置。 本节介绍这两种方案。

> [!IMPORTANT]
>  一定要先升级辅助服务器实例，然后再升级主服务器实例。 有关详细信息，请参阅本主题前面的 [升级辅助服务器实例](#UpgradeSecondary)。


####  <a name="scenario-1-upgrade-primary-server-instance-without-failover"></a><a name="Scenario1"></a>方案1：在没有故障转移的情况下升级主服务器实例
 这个方案比较简单，但导致的停机时间要比使用故障转移时间长。 主服务器实例进行简单的升级，数据库在升级期间不可用。

 服务器升级完毕后，数据库即自动回到联机状态，随即进行升级。 数据库升级完毕后，日志传送作业将继续进行。

#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>方案 2：借助故障转移升级主服务器实例
 此方案最大限度地提高了可用性，同时使停机时间降低到最短。 此方案采取向辅助服务器实例实行受控故障转移的方式，使数据库在原始主服务器实例升级期间保持可用状态。 停机时间限于故障转移所需的相对短的时间，而不是升级主服务器实例所需的时间。

 借助故障转移升级主服务器实例一般需要三个过程：执行到辅助服务器的受控故障转移，将原始主服务器实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 主服务器实例上设置日志传送。 本节后面将对这三个过程进行介绍。

> [!IMPORTANT]
>  如果计划使辅助服务器实例成为新的主服务器实例，则需要删除日志传送配置。 原始主服务器实例升级完毕后，需要重新配置从新的主服务器实例到新的辅助服务器实例的日志传送。 有关详细信息，请参阅[&#40;SQL Server&#41;中删除日志传送](remove-log-shipping-sql-server.md)。


#####  <a name="procedure-1-perform-a-controlled-failover-to-the-secondary-server"></a><a name="Procedure1"></a>步骤1：执行到辅助服务器的受控故障转移
 到辅助服务器的受控故障转移：

1.  在使用 NORECOVERY 指定的主数据库上手动执行事务日志的[结尾日志备份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。 此日志备份捕获任何尚未备份的日志记录并使数据库脱机。 请注意：数据库脱机期间，日志传送备份作业将失败。

     下面的示例在主服务器上创建 `AdventureWorks` 数据库的一个结尾日志备份。 此备份文件名为 `Failover_AW_20080315.trn`：

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

     建议您使用非重复的文件命名约定区分手动创建的备份文件和日志传送备份作业创建的备份文件。

2.  在辅助服务器上：

    1.  确保日志传送备份作业自动进行的所有备份都已应用。 若要检查哪些备份作业已应用，请使用监视服务器或主服务器和辅助服务器上的[sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql)系统存储过程。 同一文件应在 " **last_backup_file**"、" **last_copied_file**" 和 " **last_restored_file** " 列中列出。 如果尚未复制和还原任何备份文件，则请手动调用代理复制和还原作业以进行日志传送配置。

         有关启动作业的信息，请参阅 [Start a Job](../../ssms/agent/start-a-job.md)。

    2.  将您在第一步中创建的最后一个日志备份文件从文件共享复制到辅助服务器上的日志传送使用的本地位置。

    3.  还原指定 WITH RECOVERY 的最后一个日志备份以使数据库联机。 数据库联机的同时将升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

         下面的示例还原辅助数据库中的 `AdventureWorks` 数据库的结尾日志备份。 此示例使用 WITH RECOVERY 选项，该选项将使数据库联机：

        ```
        RESTORE LOG AdventureWorks 
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn' 
           WITH RECOVERY;
        GO
        ```

        > [!NOTE]
        >  对于包含多个辅助服务器的配置，还有额外的注意事项。 有关详细信息，请参阅本主题后面的 [升级多个辅助服务器实例](#MultipleSecondaries)。

    4.  将客户端从原始主服务器（服务器 A）重定向到联机辅助服务器（服务器 B），以对数据库进行故障转移。

    5.  请注意：辅助数据库在处于联机状态时，它的事务日志并未填满。 若要阻止事务日志填满，可能需要备份此日志。 如果是这样，建议您将它备份到共享位置，即备份到“备份共享” **，以便在其他服务器实例上可以还原这些备份。

#####  <a name="procedure-2-upgrade-the-original-primary-server-instance-to-sscurrent"></a><a name="Procedure2"></a>过程2：将原始主服务器实例升级到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 将原始主服务器实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]后，数据库仍将处于脱机状态且仍采用该格式。

#####  <a name="procedure-3-set-up-log-shipping-on-sscurrent"></a><a name="Procedure3"></a>步骤3：在上设置日志传送[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 剩余的升级过程取决于是否仍配置日志传送，如下所述：

-   如果保留了 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本日志传送配置，则请切换回原始主服务器实例。 有关详细信息，请参阅本节后面的 [切换回原始主服务器实例](#SwitchToOrigPrimary)。

-   如果在进行故障转移之前删除了日志传送配置，则请创建一个新的日志传送配置，其中原始辅助服务器实例是新的主服务器实例。 有关详细信息，请参阅本节后面的 [将原来的辅助服务器实例作为新的主服务器实例](#KeepOldSecondaryAsNewPrimary)。

######  <a name="to-switch-back-to-the-original-primary-server-instance"></a><a name="SwitchToOrigPrimary"></a>切换回原始主服务器实例

1.  在临时主服务器（服务器 B）上使用 WITH NORECOVERY 备份日志尾部，以创建结尾日志备份并使数据库脱机。 该结尾日志备份命名为 `Switchback_AW_20080315.trn`。例如：

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

2.  如果任何事务日志备份都是在临时主数据库上进行的，则将那些使用 WITH NORECOVERY 的日志备份（不包括在第一步中创建的结尾备份）还原到原始主服务器（服务器 A）上的脱机数据库。 第一个日志备份还原后，数据库即升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。

3.  在原始主数据库上（即在服务器 A 上）使用 WITH RECOVERY 还原结尾日志备份 `Switchback_AW_20080315.trn`，从而使数据库联机。

4.  将客户端从原始主服务器重定向到联机辅助服务器，从而故障转移回原始主数据库（位于服务器 A 上）。

 数据库联机后，原始日志传送配置将恢复。

######  <a name="to-keep-the-old-secondary-server-instance-as-the-new-primary-server-instance"></a><a name="KeepOldSecondaryAsNewPrimary"></a>保留旧的辅助服务器实例作为新的主服务器实例
 按照下面所述建立新的日志传送配置，其中原来的辅助服务器实例 B 用作主服务器，而原来的主服务器实例 A 用作新的辅助服务器：

> [!IMPORTANT]
>  在此过程开始时且在进行使数据库脱机的手动事务日志备份之前，应该已从原始主服务器上删除原来的日志传送配置。

1.  若要避免对新的辅助服务器（服务器 A）上的数据库执行完整的备份和还原，请将新的主数据库的日志备份应用到新的辅助数据库。 在示例配置中，这包括将在服务器 B 上进行的日志备份还原到服务器 A 上的数据库。

2.  备份新的主数据库（位于服务器 B 上）的日志。

3.  使用 WITH NORECOVERY 将日志备份还原到新的辅助服务器实例（服务器 A）。 第一个还原操作将数据库升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

4.  配置日志传送，使原来的辅助服务器（服务器 B）作为主服务器实例。

    > [!IMPORTANT]
    >  如果使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，请指定辅助数据库已初始化。

     有关详细信息，请参阅[配置日志传送 (SQL Server)](configure-log-shipping-sql-server.md)。

5.  将客户端从原始主服务器（服务器 A）重定向到联机辅助服务器（服务器 B），以对数据库进行故障转移。

    > [!IMPORTANT]
    >  故障转移到新的主数据库时，应确保其元数据与原始主数据库的元数据一致。 有关详细信息，请参阅在[使数据库在其他服务器实例上可用时管理元数据 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。

##  <a name="upgrading-multiple-secondary-server-instances"></a><a name="MultipleSecondaries"></a>升级多个辅助服务器实例
 下图显示了此配置，其中 A 为主服务器实例，B 和 C 都是辅助服务器实例。

 ![两台辅助服务器，无监视服务器](../media/ls-3-wayconfig-nomonitor.gif "两台辅助服务器，无监视服务器")

 本节讨论如何使用故障转移进行升级，然后再切换回原始主服务器。 如果有多个辅助服务器实例，则借助故障转移升级主实例的过程将更加复杂。 在下面的过程中，所有辅助服务器升级完毕后，主服务器故障转移到其中一个已升级的辅助数据库。 原始主服务器得到升级，然后日志传送重新故障转移到原始主服务器。

> [!IMPORTANT]
>  必须先对所有辅助服务器实例进行升级，然后再升级主服务器。

 **借助故障转移进行升级，然后切换回原始主服务器**

1.  升级全部辅助服务器实例（服务器 B 和服务器 C）。

2.  获取主数据库（位于服务器 A 上）的事务日志尾部，并使用 WITH NORECOVERY 备份此事务日志，以使该数据库脱机。

3.  通过使用 WITH RECOVERY 还原日志备份，使您计划故障转移到的辅助服务器（服务器 B）上的辅助数据库联机。

4.  在所有其他辅助服务器（服务器 C）上，通过使用 WITH NORECOVERY 还原日志备份，使辅助数据库仍处于脱机状态。

    > [!NOTE]
    >  日志传送复制和还原作业将在辅助服务器上运行，但由于新的日志备份文件不会放在备份共享中，因此这些作业不执行任何操作。

5.  将客户端从原始主服务器（服务器 A）重定向到联机辅助服务器（服务器 B），以对数据库进行故障转移。 联机数据库将成为临时主服务器，从而保持该数据库在原始主服务器（服务器 A）脱机期间仍可用。

6.  升级原始主服务器（服务器 A）。

7.  在故障转移到的数据库（在服务器 B 上）上，使用 WITH NORECOVERY 手动备份事务日志。 这将使该数据库脱机。

8.  将使用 WITH NORECOVERY 在临时主数据库（位于服务器 B 上）上创建的所有事务日志备份还原到所有其他辅助数据库（位于服务器 C 上）。 从而在原始主数据库升级后，可以继续从其进行日志传送，而无需对每个辅助数据库进行完全的数据库还原。

9. 使用 WITH RECOVERY 将临时主服务器（服务器 B）上的事务日志还原到的原始主数据库（位于服务器 A 上）。

##  <a name="redeploying-log-shipping"></a><a name="Redeploying"></a>重新部署日志传送
 如果不想使用上述过程之一迁移日志传送配置，可以通过使用主数据库的完整备份和恢复来重新初始化辅助数据库，从而从头开始重新部署日志传送。 如果数据库较小，或者在升级过程中高可用性并不是至关重要的，此方法将是个不错的选择。

 有关启用日志传送的信息，请参阅[配置日志传送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。

## <a name="see-also"></a>另请参阅
 [事务日志备份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) [应用事务日志备份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md) [日志传送表和存储过程](log-shipping-tables-and-stored-procedures.md)
