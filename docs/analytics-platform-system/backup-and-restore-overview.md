---
title: 备份和还原-并行数据仓库 |Microsoft Docs
description: 描述数据如何备份和还原为并行数据仓库 (PDW) 的工作原理。 备份和还原操作用于灾难恢复。 备份和还原还可用来将数据库从一个设备复制到另一个设备。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e95415c689fda43c2a9d118713c96d0a1d531904
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419992"
---
# <a name="backup-and-restore"></a>备份和还原

描述数据如何备份和还原为并行数据仓库 (PDW) 的工作原理。 备份和还原操作用于灾难恢复。 备份和还原还可用来将数据库从一个设备复制到另一个设备。  
    
## <a name="BackupRestoreBasics"></a>备份和还原的基础知识

PDW*数据库备份*，以便它可以用于将原始数据库还原到一台设备的格式存储的工具数据库的副本。  
  
PDW 数据库备份创建与[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)t-sql 语句，并且用于格式化[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)语句; 它不可用于任何其他用途。 备份只能还原到一台设备具有相同数量或大量的计算节点。  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW 使用 SQL Server 备份技术备份和还原设备数据库。 SQL Server 备份选项已预先配置为使用备份压缩。 不能设置压缩、校验和、块大小和缓冲区计数等备份选项。  
  
数据库备份存储在一个或多个备份的服务器，客户网络中存在的。  PDW 写入用户数据库备份以并行直接从计算节点一台备份服务器，并将并行中的用户数据库备份从备份服务器直接还原到计算节点。  
  
备份 Windows 文件系统中存储备份的服务器上作为一组文件。 PDW 数据库备份只能还原到 PDW。 但是，您可以通过使用标准 Windows 文件备份过程存档数据库备份从备份服务器到另一个位置。 有关备份服务器的详细信息，请参阅[Acquire 和配置备份服务器](acquire-and-configure-backup-server.md)。  
  
## <a name="BackupTypes"></a>数据库的备份类型

有两种类型的需要备份的数据： 用户数据库和系统数据库 （例如，主数据库）。 PDW 不会备份事务日志。  
  
完整数据库备份是整个 PDW 数据库的备份。 这是默认备份类型。 用户数据库的完整备份包含数据库用户和数据库角色。 主备份包含登录名。  
  
差异备份中包含的所有更改自上次完整备份。 差异备份所需的时间通常比完整备份所需的时间少，并且可以更频繁地执行。 多个差异备份基于同一完整备份，每个差异在上一个差异中包含的所有更改。  
  
例如，可以创建完整备份每周和每日差异备份。 若要还原用户数据库、 完整备份以及上次差异 （如果存在） 需要还原。  
  
差异备份仅支持为用户数据库。 备份 master 始终是完整备份。  
  
若要备份整个设备，你需要执行的所有用户数据库的备份和 master 数据库的备份。  
  
## <a name="BackupProc"></a>数据库备份过程

下图显示数据库备份期间的数据的流。  
  
![PDW 备份过程](media/backup-process.png "PDW 备份过程")  
  
备份过程的工作方式如下：  
  
1.  用户提交到控制节点的 BACKUP DATABASE tsql 语句。  
  
    -   备份为完整或差异备份。  
  
2.  对于用户数据库，控制节点 （MPP 引擎） 创建的分布式的查询计划执行并行数据库备份。  
  
3.  每个节点中备份的副本涉及到使用 SQL Server 备份功能备份服务器其备份文件。  
  
    -   每个节点所涉及到备份服务器的副本的一个备份文件。  
  
    -   用户数据库备份 （完整或差异） 包括存储上每个计算节点和备份的数据库用户和数据库角色的数据库的部分备份。  
  
4.  设备使用 InfiniBand 网络并行执行备份。  
  
    -   PDW 并行执行每个完整和差异备份。 但是，多个数据库备份不能同时运行。 备份的每个请求必须等待以前提交的备份来完成。  
  
    -   Master 数据库的备份仅备份从控制节点数据。 这种备份类型是按顺序执行。  
  
5.  PDW 数据库备份是驻留在设备以外的目录中存储的文件组。 目录名称指定为网络路径和目录名称。 目录不能为本地路径，并且它不能在设备上。  
  
6.  备份完成后，可用于 Windows 文件系统的备份目录复制到其他位置，如果所需的。  
  
    -   备份只能还原到 PDW 设备具有的计算节点数量相等或更高版本。  
  
    -   在执行还原之前，不能更改备份的名称。 备份目录的名称必须匹配备份的原始名称的名称。 备份的原始名称位于 backup.xml 文件中的备份目录中。 若要将数据库还原到不同的名称，可以在还原命令中指定新名称。 例如： `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`。  
  
## <a name="RestoreModes"></a>数据库还原模式

完整数据库还原重新创建数据库备份中使用的数据的 PDW 数据库。 通过首先还原完整备份，然后根据需要将还原一个差异备份执行数据库还原。 数据库还原包含数据库用户和数据库角色。  
  
标头仅还原返回数据库的标头信息。 它不会还原到该设备数据。  
  
将设备还原是还原整个设备。 这包括还原所有用户数据库和 master 数据库。  
  
## <a name="RestoreProc"></a>还原过程

下图显示在数据库还原过程中的数据的流。  
  
![还原过程](media/restore-process.png "还原过程")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>还原到相同数量的计算节点 * * 的设备  
  
还原数据时，设备检测到源设备和目标设备上的计算节点的数。 如果这两个设备有相同数目的计算节点，在还原过程的工作方式如下：  
  
1.  要还原的数据库备份是可在非设备备份服务器上的 Windows 文件共享上。 为了获得最佳性能，此服务器连接到设备 InfiniBand 网络。  
  
2.  用户提交[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)到控制节点的 tsql 语句。  
  
    -   完整还原或标头还原，还原。 完整还原将还原完整备份，然后根据需要还原差异备份。  
  
3.  控制节点 （MPP 引擎） 创建的分布式的查询计划，以执行并行数据库还原。  
  
    -   SQL ServerPDW 并行执行用户数据库的还原。 但是，多个数据库的备份和还原是不同时运行。 MPP 引擎将放在队列中; 每个 restore 语句它必须等待以前提交的备份和还原完成的请求。  
  
    -   Master 数据库的还原仅将数据还原到控制节点;按顺序执行还原。  
  
    -   标头信息的还原是一个快速操作，不会将任何数据还原到的计算或控制节点。 相反，控制节点作为查询输出中返回的结果。  
  
4.  备份文件复制到正确的计算节点并行情况下，通常通过设备 InfiniBand 网络。  
  
5.  每个计算节点将还原用户数据库的相应部分。 如果还原的任何未成功完成，所有数据库中删除并还原未成功完成。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>还原到更多的计算节点的设备  
  
将备份还原到计算节点数更大的设备会与计算节点数成比例地增加分配的数据库大小。  
  
例如，60 GB 数据库从 2 节点设备 (每个节点 30 GB) 还原到 6 节点设备，当 SQL Server PDW 6 节点设备上创建 180 GB 数据库 （6 个节点 30 gb 每个节点）。 SQL Server PDW 最初将数据库还原到 2 个节点以匹配源配置，然后重新分发到所有 6 个节点数据。  
  
重新分发之后, 每个计算节点将包含较少的实际数据和更多可用空间比与较小源设备上的每个计算节点。 使用附加空间可将更多数据添加到数据库。 如果还原的数据库大小大于所需值，则可以使用[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)收缩数据库文件大小。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|备份和还原任务|Description|  
|---------------------------|---------------|  
|为备份服务器准备服务器。|[获取和配置备份服务器 ](acquire-and-configure-backup-server.md)|  
|备份数据库。|[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|将数据库还原。|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
