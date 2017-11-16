---
title: "备份压缩 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
caps.latest.revision: "51"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 817ca0481f0629aac260c79a2ada21a33e54772c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="backup-compression-sql-server"></a>备份压缩 (SQL Server)
  本主题介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的压缩，包括限制、压缩备份时的性能折中、备份压缩的配置以及压缩率。  以下 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本支持备份压缩：企业版、标准版和开发人员版。  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的每个版本和更高版本都可以还原已压缩的备份。 
 
  
##  <a name="Benefits"></a> 优势  
  
-   因为相同数据的压缩的备份比未压缩备份小，所以压缩备份所需的设备 I/O 通常较少，因此通常可大大提高备份速度。  
  
     有关详细信息，请参阅本主题后面的 [压缩备份的性能影响](#PerfImpact)。  
  
  
##  <a name="Restrictions"></a> 限制  
 压缩的备份具有以下限制条件：  
  
-   压缩的备份和未压缩的备份不能共存于一个介质集中。  
  
-   早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法读取压缩的备份。  
  
-   NTbackup 无法共享包含压缩的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的磁带。  
  
  
##  <a name="PerfImpact"></a> 压缩备份的性能影响  
 默认情况下，压缩会显著增加 CPU 的使用，并且压缩进程所消耗的额外 CPU 可能会对并发操作产生不利影响。 因此，你可能需要在会话中创建低优先级的压缩备份，其 CPU 使用率受[资源调控器](../../relational-databases/resource-governor/resource-governor.md)限制。 有关详细信息，请参阅本主题后面的 [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制。  
  
 若要很好地了解备份 I/O 的性能表现，可以通过评估以下类型的性能计数器来分别考察进入设备或来自设备的备份 I/O：  
  
-   Windows I/O 性能计数器，例如物理磁盘计数器  
  
-   **SQLServer:备份设备** 对象的 [设备吞吐量（字节/秒）](../../relational-databases/performance-monitor/sql-server-backup-device-object.md) 计数器  
  
-   **SQLServer:数据库** 对象的 [备份/还原吞吐量/秒](../../relational-databases/performance-monitor/sql-server-databases-object.md) 计数器  
  
 有关 Windows 计数器的信息，请参阅 Windows 帮助。 有关如何使用 SQL Server 计数器的信息，请参阅 [使用 SQL Server 对象](../../relational-databases/performance-monitor/use-sql-server-objects.md)。  
  
   
##  <a name="CompressionRatio"></a> 计算压缩的备份的压缩率  
 若要计算备份的压缩率，请使用 **backupset** 历史记录表的 **backup_size** 列和 [compressed_backup_size](../../relational-databases/system-tables/backupset-transact-sql.md) 列中有关此备份的值，如下所示：  
  
 **backup_size**:**compressed_backup_size**  
  
 例如，3:1 的压缩率表明您可以节省大约 66% 的磁盘空间。 若要查询这些列，可以使用以下 Transact-SQL 语句：  
  
```  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 压缩备份的压缩率取决于所压缩的数据。 有多种因素会影响所获得的压缩率。 主要因素包括：  
  
-   数据类型。  
  
     字符数据的压缩率要高于其他类型的数据。  
  
-   页面上各行间数据的一致性。  
  
     通常，如果某页包含多个行，而其中的某个字段包含相同的值，则该值可获得较大的压缩。 相反，对于包含随机数据或者每页只有一个很大的行的数据库，压缩备份的大小几乎与未压缩的备份相同。  
  
-   数据是否加密。  
  
     与未加密数据相比，同样的加密数据的压缩率要小得多。 如果使用透明数据加密来加密整个数据库，则压缩备份不会将数据库大小减小很多，甚至根本不会减小。  
  
-   数据库是否压缩。  
  
     如果压缩数据库，则压缩备份不会将大小减小很多，甚至根本不会减小。  
  
  
##  <a name="Allocation"></a> 为备份文件分配空间  
 对于压缩的备份，最终备份文件的大小取决于数据可压缩程度，这在备份操作完成之前是未知的。  因此，默认情况下，在使用压缩备份数据库时，数据库引擎将预先分配算法用于备份文件。 此算法为备份文件预先分配数据库大小的预定义的百分比。 如果在备份操作过程中需要更多空间，则数据库引擎会增大该文件。 如果最终大小小于分配的空间，则在备份操作结束时，数据库引擎会将该文件收缩到备份的实际的最终大小。  
  
 若要允许备份文件仅在需要时增大以便达到其最终大小，则使用跟踪标志 3042。 跟踪标志 3042 导致备份操作绕过默认的备份压缩预先分配算法。 如果您需要仅分配压缩的备份所需的实际大小以便节约空间，则此跟踪标志将很有用。 但是，使用此跟踪标志可能会导致轻微的性能损失（在备份操作期间损失可能会增加）。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [配置备份压缩 (SQL Server)](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [备份概述 (SQL Server)](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  
