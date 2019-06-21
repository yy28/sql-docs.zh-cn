---
title: 使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原 | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 625eccb976c500dcacaa5612ca41bac8b638fbed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62516221"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![“备份到 Azure blob”图](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "“备份到 Azure blob”图")  
  
 本主题介绍将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份到 [Microsoft Azure Blob 存储服务](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)和从中还原。 它还总结了使用 Microsoft Azure Blob 服务存储 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的好处。  
  
 SQL Server 支持通过以下方式将备份存储到 Microsoft Azure Blob 存储服务：  
  
-   **管理存储到 Microsoft Azure 的备份：** 使用与用于备份到磁盘和磁带相同的方法，即可通过将 URL 指定为备份目标立即备份到 Microsoft Azure 存储。 可使用此功能手动备份或配置自己的备份策略，如同对于本地存储或其他站点外选项所做的一样。 此功能也称为 **SQL Server 备份到 URL**。 有关详细信息，请参阅 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。 SQL Server 2012 SP1 CU2 或更高版本中提供此功能。 此功能在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中得到了增强，以便通过使用块 Blob、共享访问签名和条带化提高性能和改进功能。  
  
    > [!NOTE]  
    >  对于版本低于 SQL Server 2012 SP1 CU2 的 SQL Server，可使用外接程序“SQL Server 备份到 Microsoft Azure 工具”快速轻松地向 Microsoft Azure 存储创建备份。 有关详细信息，请参阅 [下载中心](https://go.microsoft.com/fwlink/?LinkID=324399)。  
  
-   **Azure Blob 存储中的数据库文件的文件快照备份** 通过使用 Azure 快照， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文件快照备份可以通过使用 Azure Blob 存储服务为存储的数据库文件提供几乎即时的备份和还原。 此功能可以简化备份和还原策略，而且它还支持时间点还原。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。 SQL Server 2016 或更高版本中提供此功能。  
  
-   **使 SQL Server 管理 Microsoft Azure 备份：** 通过配置 SQL Server，来管理备份策略并为一个或多个数据库安排备份，或根据实例级别设置默认值。 此功能被称为 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** 。 有关详细信息，请参阅 [Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。 SQL Server 2014 或更高版本中提供此功能。  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>将 Microsoft Azure Blob 服务用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的好处  
  
-   灵活、可靠、无限制的站点外存储：在 Microsoft Azure Blob 服务上存储备份是一种既便捷灵活又易于访问的站点外存储方法。 为您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份创建站点外存储就像修改您的现有脚本/作业一样简单。 站点外存储位置通常应远离生产数据库位置，以防止出现同时影响站点外和生产数据库位置的一个灾难。 通过选择地理复制 Blob 存储区，您在发生可能影响整个区域的灾难时多了一层额外的保护。 此外，备份副本随时随地可用，并可以轻松访问它们来执行还原。  
  
    > [!IMPORTANT]  
    >  在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中使用块 blob 可以条带化备份集，支持对大小高达 12.8 TB 的文件进行备份。  
  
-   备份存档：在对备份进行存档时，Microsoft Azure Blob 存储服务能够提供可替代常用磁带存储方式的更好方式。 磁带存储可能需要物理传输到站点外设施并采取措施来保护介质。 在 Microsoft Azure Blob 存储区中存储你的备份可以提供一个即时、高度可用、耐久的存档方案。  
  
-   无硬件管理开销：没有有关 Microsoft Azure 服务的硬件管理开销。 Microsoft Azure 服务管理硬件并支持地理复制以提供冗余和防止硬件故障。  
  
-   当前对于在 Microsoft Azure 虚拟机中运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，可以通过创建附加的磁盘来备份到 Microsoft Azure Blob 存储服务。 但是，对于可以附加到 Microsoft Azure 虚拟机的磁盘数有限制。 限制值为：超大实例最多使用 16 个磁盘，较小的实例可使用的磁盘则更少。 通过允许直接备份到 Microsoft Azure Blob 存储区，你可以绕过 16 个磁盘的限制。  
  
     此外，目前存储在 Microsoft Azure Blob 存储服务中的备份文件直接可用于本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或在 Microsoft Azure 虚拟机中运行的其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而无需进行数据库附加/分离或下载并附加 VHD。  
  
-   成本权益：只需要为使用的服务付费。 可以作为经济合算的站点外备份存档方案。 有关详细信息和链接，请参阅 [Microsoft Azure 计费注意事项](#Billing) 一节。  
  
##  <a name="Billing"></a> Microsoft Azure 计费注意事项：  
 了解 Microsoft Azure 存储成本使你能够预测在 Microsoft Azure 中创建和存储备份的成本。  
  
 [Microsoft Azure 价格计算器](https://go.microsoft.com/fwlink/?LinkId=277060) 可以帮助估算你的成本。  
  
 **存储：** 根据所使用的空间以及分级比例和冗余级别来计算费用。 有关详细信息和最新信息，请参阅 **定价详细信息** 文章中的[“数据管理”](https://go.microsoft.com/fwlink/?LinkId=277059) 一节。  
  
 **数据传输：** Microsoft Azure 的入站数据传输是免费的。 出站传输要支付带宽使用费用，并根据渐变的区域特定标准来计算费用。 有关详细信息，请参阅“定价详细信息”文章中的 [数据传输](https://go.microsoft.com/fwlink/?LinkId=277061) 一节。  
  
## <a name="see-also"></a>另请参阅  

[SQL Server 备份到 URL 最佳实践和故障排除](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[教程：将 Microsoft Azure Blob 存储服务用于 SQL Server 2016 数据库](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[SQL Server 备份到 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
