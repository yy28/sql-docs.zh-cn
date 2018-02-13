---
title: "备份和还原"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "描述数据如何备份和还原的 SQL Server 并行数据仓库 (PDW) 的工作原理。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: d4669957-270a-4e50-baf3-14324ca63049
caps.latest.revision: 
ms.openlocfilehash: 06863b600ed62d795db82aa5aa3ae5c88578833a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="backup-and-restore"></a>备份和还原
描述数据如何备份和还原的 SQL Server 并行数据仓库 (PDW) 的工作原理。 备份和还原操作用于灾难恢复。 备份和还原还可将数据库从一个设备复制到另一个设备。  
    
## <a name="BackupRestoreBasics"></a>备份和还原的基础知识  
PDW*数据库备份*是一份装置数据库，以便它可以用于将原始数据库还原到设备的格式存储。  
  
使用创建 PDW 数据库备份[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)t-sql 语句，并且用于格式化[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)语句; 它用于任何其他用途是不可用。 备份只能还原到设备以相同的数字或更多的计算节点。  
  
<!-- MISSING LINKS

The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  

-->
  
PDW 使用 SQL Server 的备份技术来备份和还原设备的数据库。 SQL Server 备份选项已预先配置为使用备份压缩。 不能设置如压缩、 校验和、 块大小以及缓冲区计数的备份选项。  
  
数据库备份存储在一个或多个备份服务器，它存在于客户网络上。  PDW 将用户数据库备份并行直接从计算节点写入一个备份服务器，并将并行的用户数据库备份直接从备份服务器还原到计算节点。  
  
备份 Windows 文件系统中存储备份的服务器上作为一组文件。 PDW 数据库备份仅可以还原到 PDW 中。 但是，您可以通过使用标准 Windows 文件备份过程进行存档从备份服务器到另一个位置的数据库备份。 有关备份服务器的详细信息，请参阅[获取和配置备份服务器](acquire-and-configure-backup-server.md)。  
  
## <a name="BackupTypes"></a>数据库备份类型  
有两种类型的要求执行备份的数据： 用户数据库和系统数据库 （例如，master 数据库）。 PDW 不备份事务日志。  
  
完整数据库备份是整个 PDW 数据库备份。 这是默认的备份类型。 用户数据库的完整备份包括数据库用户和数据库角色。 Master 数据库的备份包括登录名。  
  
差异备份包含的所有更改自上次完整备份。 差异备份通常采用较少的时间比完全备份，并可以更频繁地执行。 多个差异备份都基于相同的完整备份，每个差异在上一个差异包括的所有更改。  
  
例如，你可以创建完整备份每周和每日差异备份。 若要还原用户数据库、 完整备份加上最后一个差异 （如果存在） 需要还原。  
  
差异备份仅支持的用户数据库。 Master 数据库的备份始终是完整备份。  
  
若要备份整个设备，你需要执行的所有用户数据库的备份，而 master 数据库的备份。  
  
## <a name="BackupProc"></a>数据库备份过程  
下图在数据库备份期间显示的数据的流。  
  
![PDW 备份过程](media/backup-process.png "PDW 备份过程")  
  
备份过程的工作方式如下：  
  
1.  用户将提交到控制节点的 BACKUP DATABASE tsql 语句。  
  
    -   该备份是完整或差异备份。  
  
2.  对于用户数据库，控制节点 （MPP 引擎） 创建分布式的查询计划，以执行并行数据库备份。  
  
3.  每个节点的备份副本涉及到使用 SQL Server 备份功能备份服务器其备份文件。  
  
    -   每个节点涉及到备份服务器的副本的一个备份文件。  
  
    -   （完整或差异） 的用户数据库备份包括存储上每个计算节点和备份的数据库用户和数据库角色的数据库的部分备份。  
  
4.  设备在并行使用 InfiniBand 网络执行备份。  
  
    -   PDW 并行执行每个完整和差异备份。 但是，多个数据库备份不同时运行。 每个备份请求必须等待以前提交的备份完成。  
  
    -   Master 数据库的备份仅备份从管理节点数据。 这种备份类型是按顺序执行。  
  
5.  PDW 数据库备份是一组关闭设备所在的目录中存储的文件。 目录名称指定为网络路径和目录的名称。 目录不能为本地路径，并且它不能在设备上。  
  
6.  完成备份后，你可以使用 Windows 文件系统将备份目录复制到另一个位置，如果需要。  
  
    -   备份可以还原到 PDW 工具具有相等或更高版本的计算节点数目。  
  
    -   不能在执行还原之前更改的备份的名称。 备份目录的名称必须匹配的备份的原始名称的名称。 中的备份目录的 backup.xml 文件位于的备份的原始名称。 若要将数据库还原到不同的名称，可以在 restore 命令中指定新名称。 例如： `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`。  
  
## <a name="RestoreModes"></a>数据库还原模式  
完整数据库还原重新创建 PDW 数据库在数据库备份过程中使用的数据。 通过首先还原完整备份，然后根据需要还原一个差异备份执行数据库还原。 数据库还原包括数据库用户和数据库角色。  
  
标头仅还原返回数据库的标头信息。 它不将数据还原到设备。  
  
设备还原是还原整个设备。 这包括还原所有用户数据库和 master 数据库。  
  
## <a name="RestoreProc"></a>还原过程  
下图显示在数据库还原过程中的数据流。  
  
![还原过程](media/restore-process.png "还原过程")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>还原到设备，但有相同数量的计算节点 * *  
  
还原数据时，设备检测到源设备和目标设备上的计算节点的数。 如果这两个设备中有相同数目的计算节点，但在还原过程的工作方式如下：  
  
1.  要还原的数据库备份是在非设备备份服务器上的 Windows 文件共享上可用。 为了获得最佳性能，此服务器通常会连接到的设备 InfiniBand 网络。  
  
2.  用户提交[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)到控制节点的 tsql 语句。  
  
    -   还原为完整还原或标头还原。 完整还原还原完整备份，然后根据需要还原差异备份。  
  
3.  控制节点 （MPP 引擎） 创建分布式的查询计划，以执行并行数据库还原。  
  
    -   SQL ServerPDW 并行执行用户数据库的还原。 但是，多个数据库的备份和还原不会运行同时。 MPP 引擎将放入队列; 每个 restore 语句它必须等待以前提交的备份和还原完成的请求。  
  
    -   还原的 master 数据库仅将数据还原到管理节点中;按顺序执行还原。  
  
    -   标头信息的还原是一个快速操作，不将任何数据还原到计算或控件节点。 相反，控制节点作为查询输出返回的结果。  
  
4.  备份文件会复制到正确的计算节点并行，通常通过设备 InfiniBand 网络。  
  
5.  每个计算节点还原其部分用户数据库。 如果还原的任何未成功完成，所有数据库获取删除和还原未成功完成。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>还原到设备，但有更多计算节点  
  
将备份还原到设备，但有更多计算节点增长与计算节点数成比例的已分配的数据库大小。  
  
例如，当 2 节点设备 (每个节点的 30 GB) 为 60 GB 的数据库还原到一个 6 节点设备中，SQL Server PDW 就在 6 节点设备上创建一个 180 GB 的数据库 （6 个节点有 30 GB 每个节点）。 SQL Server PDW 最初将数据库还原到 2 个节点以匹配源配置，然后重新分配到所有 6 节点数据。  
  
重新分发后每个计算节点将包含较少的实际数据和比在较小的源设备上每个计算节点的更多可用空间。 使用其他空间将更多的数据添加到数据库。 如果还原的数据库大小大于所需值，则可以使用[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)收缩数据库文件大小。  
  
## <a name="related-tasks"></a>相关任务  
  
|备份和还原任务|Description|  
|---------------------------|---------------|  
|准备一台服务器作为备份服务器。|[获取和配置备份服务器 ](acquire-and-configure-backup-server.md)|  
|备份数据库。|[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|还原的数据库。|[还原数据库](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    
<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
