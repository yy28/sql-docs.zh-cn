---
title: 管理 DQS 数据库
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ce7b0239168a0a85e5d0f559b042dac0562ead94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246977"
---
# <a name="manage-dqs-databases"></a>管理 DQS 数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本节提供了有关可在 DQS 数据库上执行的数据库管理活动（例如备份/还原或分离/附加）的信息。  
  
##  <a name="backup-and-restore-the-dqs-databases"></a><a name="BackupRestore"></a> 备份和还原 DQS 数据库  
 SQL Server 数据库的备份和还原是数据库管理员经常要执行的操作，以便通过从备份数据库恢复数据在出现灾难时避免数据丢失。 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 主要由两个 SQL Server 数据库实现：DQS_MAIN 和 DQS_PROJECTS。 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 数据库的备份和还原过程与其他 SQL Server 数据库相似。有三个与 DQS 数据库的备份和还原相关联的挑战：  
  
-   DQS 数据库的备份和还原操作必须同步。 否则，还原的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 将不会正常工作。  
  
-   这两个 DQS 数据库（DQS_MAIN 和 DQS_PROJECTS）包含程序集和其他复杂对象，而非只是简单数据库对象（例如表和存储过程）。  
  
-   在 DQS 数据库之外有一些实体，这些实体必须存在 DQS 数据库才能像 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]一样正常工作，尤其是两个 SQL Server 登录名（##MS_dqs_db_owner_login## 和 ##MS_dqs_service_login##）以及 master 数据库中的一个初始化存储过程 (DQInitDQS_MAIN)。  
  
 有关 SQL Server 中备份和还原的详细信息，请参阅 [SQL Server 数据库的备份和还原](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
### <a name="default-autogrowth-size-and-recovery-model-for-the-dqs-databases"></a>DQS 数据库的默认自动增长大小和恢复模式  
 防止 DQS 数据库和事务日志无限增长以致有可能填满硬盘：  
  
-   DQS 数据库的默认 **“自动增长”** 大小设置为 10%。  
  
-   DQS 数据库的默认恢复模式设置为“简单” ****。 在“简单”恢复模式下，会尽量少地记录事务日志，而且在完成事务后会自动截断日志以释放事务日志（.ldf 文件）中的空间。 有关简单恢复模式的详细信息，请参阅[完整数据库备份 (SQL Server)](../relational-databases/backup-restore/full-database-backups-sql-server.md)。  
  
> [!IMPORTANT]
>  -   在“简单”恢复模式中，日志记录长时间处于活动状态时（例如，占用时间很长的事务），日志截断可能被延迟，因此可能填满事务日志。 此外，日志截断并不减小物理日志文件（.ldf 文件）的大小。 若要减少物理日志文件的大小，需要收缩日志文件。 有关如何解决涉及事务日志的问题的信息，请参阅[事务日志 &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md) 或 [https://go.microsoft.com/fwlink/?LinkId=237446](https://go.microsoft.com/fwlink/?LinkId=237446) 上的 Microsoft 技术支持文章。  
> -   必须定期执行 DQS 数据库的完整或差异备份，同时备份事务日志以执行时间点数据恢复。 有关详细信息，请参阅[完整数据库备份 (SQL Server)](../relational-databases/backup-restore/full-database-backups-sql-server.md) 和 [备份事务日志 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)。  
  
##  <a name="detachattach-the-dqs-databases"></a><a name="DetachAttach"></a> 分离/附加 DQS 数据库  
 如果您想要将 DQS 数据库更改到同一台计算机上的其他 SQL Server 实例或移动数据库，则可以分离 DQS 数据库的数据和事务日志文件，然后将这些数据库重新附加到 SQL Server 的同一个实例或其他实例。  
  
 有关在 SQL Server 中分离和附加数据库之前或在此过程中要考虑的事项的详细信息，请参阅[数据库分离和附加 (SQL Server)](../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明如何备份和还原 DQS 数据库。|[备份和还原 DQS 数据库](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|介绍如何分离和附加 DQS 数据库。|[分离数据库和附加 DQS 数据库](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>另请参阅  
 [dqs 管理](../data-quality-services/dqs-administration.md)  
  
  
