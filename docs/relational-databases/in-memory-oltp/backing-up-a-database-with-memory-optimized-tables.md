---
title: 使用内存优化表备份数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 35c700c5f9ada3fbe9426a1e7b99f6a791737e25
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34328968"
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>使用内存优化表备份数据库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  内存优化表在定期数据库备份过程中进行备份。 对于基于磁盘的表，数据和差异文件对的 CHECKSUM 在数据库备份过程中进行验证，以检测存储损坏。  
  
> [!NOTE]  
>  在备份期间，如果检测到内存优化文件组中的一个或多个文件存在校验和错误，备份操作会失败。 在这种情况下，必须从最新的已知良好备份还原数据库。  
>   
>  如果您没有备份，可从内存优化表和基于磁盘的表导出数据，然后在删除并重新创建数据库之后重新加载数据。  
  
 具有一个或多个内存优化表的数据库的完整备份包括基于磁盘的表（如果有）的已分配存储、活动事务日志以及内存优化表的数据和差异文件对（也称为检查点文件对）。 但是，如 [内存优化表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)中所述，内存优化表使用的存储可以比其在内存中的大小大得多，会影响数据库备份的大小。  
  
## <a name="full-database-backup"></a>完整数据库备份  
 此讨论侧重于只有持久内存优化表的数据库的数据库备份，因为基于磁盘的表的备份过程是相同的。 内存优化文件组中的检查点文件对可能处于各种状态。 下表介绍备份的文件部分。  
  
|检查点文件对状态|Backup|  
|--------------------------------|------------|  
|PRECREATED|仅文件元数据|  
|UNDER CONSTRUCTION|仅文件元数据|  
|ACTIVE|文件元数据加上使用的字节|  
|MERGE TARGET|仅文件元数据|  
|等待日志截断|文件元数据加上使用的字节|  
  
 有关检查点文件对状态的说明，请参阅 [sys.dm_db_xtp_checkpoint_files (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 及其列 state_desc。  
  
 具有一个或多个内存优化表的数据库备份的大小通常大于其在内存中的大小，但小于其磁盘上存储。 额外大小取决于删除的行数及其他因素。  
  
### <a name="estimating-size-of-full-database-backup"></a>估计完整数据库备份的大小  
  
> [!IMPORTANT]  
>  不建议使用 BackupSizeInBytes 值来估计内存中 OLTP 的备份大小。  
  
 第一个工作负荷方案适用于（主要）插入。 在此方案中，大多数数据文件处于“活动”状态，已完全加载，且删除的行非常少。 数据库备份的大小接近于内存中的数据大小。  
  
 第二个工作负荷方案适用于频繁的插入、删除和更新操作。 在最坏的情况下，考虑已删除的行后，每个检查点文件对都已加载 50%。 数据库备份的大小至少是内存中的数据大小的 2 倍。  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>具有内存优化表的数据库的差异备份  
 如 [内存优化表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)中所述，针对内存优化表的存储由数据和差异文件构成。 具有内存优化表的数据库的差异备份包含下列数据：  
  
-   用于存储基于磁盘的表的文件组的差异备份不会受到内存优化表是否存在的影响。  
  
-   活动事务日志与在完整数据库备份中相同。  
  
-   对于内存优化数据文件组，差异备份使用与完整数据库备份相同的算法标识用于备份的数据和差异文件，但它之后会筛选出文件的子集，如下所示：  
  
    -   数据文件包含新插入的行，并且在该文件已满时，它会关闭并且标记为只读。 只有在上次完整数据库备份后关闭了数据文件的情况下，才备份该数据文件。 差异备份仅备份包含自上次完整数据库备份后插入的行的数据文件。 例外情况是，某些插入的行可能已标记垃圾回收或已进行垃圾回收的更新和删除情形。  
  
    -   差异文件存储对已删除数据行的引用。 因为任何将来的事务都可能会删除行，所以，可在其生命周期中随时修改差异文件，该差异文件永远不会关闭。 差异文件始终备份。 差异文件通常使用不到 10% 的存储空间，因此，差异文件对差异备份大小的影响很小。  
  
 如果内存优化表在您的数据库大小中占据很大比例，则差异备份可显著减小数据库备份大小。 对于典型 OLTP 工作负荷，差异备份显著小于完整数据库备份。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表的备份、还原和恢复](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
