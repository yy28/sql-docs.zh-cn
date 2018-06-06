---
title: 备份已启用拉伸的数据库 (Stretch Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, backing up
- backups (Stretch Database)
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 512d4908213084555019c20628307309229d2b76
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34772753"
---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>备份已启用延伸的数据库 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 数据库备份有助于你从许多类型的故障、错误和灾难中恢复。  
  
 -   必须对已启用延伸的 SQL Server 数据库进行备份。  
      
 -   Microsoft Azure 将自动备份 Stretch Database 已从 SQL Server 迁移到 Azure 的远程数据。  

> [!TIP]
> 备份仅仅是完整的高可用性和业务连续性解决方案的一部分。 有关高可用性的详细信息，请参阅 [高可用性解决方案](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)。
   
## <a name="back-up-your-sql-server-data"></a>备份 SQL Server 数据  
  
若要备份已启用延伸的 SQL Server 数据库，可以继续使用目前所用的 SQL Server 备份方法。 有关详细信息，请参阅 [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。
  
 已启用延伸的 SQL Server 数据库备份只包含该备份运行时所处时间点的本地数据和符合迁移条件的数据。 （符合条件的数据是指尚未迁移，但会根据表的迁移设置迁移到 Azure 的数据。）这称为**浅表**备份，这种备份不会包括已迁移到 Azure 的数据。  
  
## <a name="back-up-your-remote-azure-data"></a>备份远程 Azure 数据   
  
Microsoft Azure 将自动备份 Stretch Database 已从 SQL Server 迁移到 Azure 的远程数据。    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>Azure 可降低自动备份时数据丢失的风险  
Azure 上的 SQL Server Stretch Database 服务通过自动存储快照（至少每隔 8 小时）保护你的远程数据库。 每张快照将保留 7 天，为你提供一系列可能的还原点。  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>Azure 可降低地域冗余带来的数据丢失的风险  
Azure 数据库备份存储在地域冗余 Azure 存储 (RA-GRS) 上，因此默认为地域冗余。 地域冗余存储会将你的数据复制到距主要区域数百英里的次要区域。 你的数据会在主要区域和次要区域中跨单独的容错域和升级域分别复制三次。 这可确保即使遇到整个区域停电或致使 Azure 其中一个区域不可用的灾难时，你的数据仍是持久的。

### <a name="stretchRPO"></a>Stretch Database 通过暂时保留已迁移行来降低 Azure 数据的数据丢失风险
Stretch Database 将符合条件的行从 SQL Server 迁移至 Azure 后，其会将这些行保留到临时表中（至少 8 小时）。 如果还原 Azure 数据库的备份，Stretch Database 将使用保存在临时表中的行来协调 SQL Server 和 Azure 的数据库。

还原 Azure 数据的备份后，必须运行 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 存储过程，重新将已启用延伸的 SQL Server 数据库连接至远程 Azure 数据库。 当你运行 **sys.sp_rda_reauthorize_db**时，Stretch Database 将自动协调 SQL Server 和 Azure 的数据库。

若要增加 Stretch Database 暂时保留到临时表中的已迁移数据的小时数，运行 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 存储过程并指定大于 8 的小时数。 若要确定要保留数据的数量，请考虑以下因素：
-   Azure 自动备份的频率（至少每隔 8 小时）。
-   出现问题后识别问题和决定恢复备份所需的时间。
-   Azure 还原操作的持续时间。

> [!NOTE]
> 增加 Stretch Database 暂时保留到临时表中的已迁移数据的数量会增加 SQL Server 所需的空间大小。

若要查看 Stretch Database 暂时保留到临时表中的数据的小时数，请运行 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)存储过程。

## <a name="see-also"></a>另请参阅  
[还原已启用延伸的数据库](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [对 Stretch Database 进行管理和故障排除](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  
