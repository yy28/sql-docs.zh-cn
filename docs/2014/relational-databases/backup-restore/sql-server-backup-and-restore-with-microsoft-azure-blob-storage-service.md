---
title: SQL Server Azure Blob 存储服务进行备份和还原 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38c92e397c971f6e9976bb857c63410fa60b7e85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75232434"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>使用 Azure Blob 存储服务进行 SQL Server 备份和还原
  本主题介绍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如何从[Azure Blob 存储服务](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)进行备份和还原。 它还汇总了使用 Azure Blob 服务存储[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份的好处。  
  
 SQL Server 支持通过以下方式将备份存储到 Azure Blob 存储服务：  
  
-   **管理你的备份到 Azure：** 使用用于备份到磁盘和磁带的相同方法，现在可以通过指定 URL 作为备份目标来备份到 Azure 存储。  可使用此功能手动备份或配置自己的备份策略，如同对于本地存储或其他站点外选项所做的一样。 此功能也称为 **SQL Server 备份到 URL**。 有关详细信息，请参阅 [SQL Server 备份到 URL](sql-server-backup-to-url.md)。 SQL Server 2012 SP1 CU2 或更高版本中提供此功能。  
  
    > [!NOTE]  
    >  对于之前 SQL Server 2014 的 SQL Server 版本，可以使用 "备份到 Azure" 工具 SQL Server 外接程序快速轻松地创建 Azure 存储备份。 有关详细信息，请参阅 [下载中心](https://go.microsoft.com/fwlink/?LinkID=324399)。  
  
-   **让 SQL Server 管理 Azure 的备份：** 配置 SQL Server 管理备份策略，并为单个数据库或多个数据库安排备份，或在实例级别设置默认值。 此功能称为**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**。 有关详细信息，请参阅[SQL Server 托管备份到 Azure](sql-server-managed-backup-to-microsoft-azure.md)。 SQL Server 2014 或更高版本中提供此功能。  
  
## <a name="benefits-of-using-the-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>使用 Azure Blob 服务进行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份的好处  
  
-   灵活、可靠和无限制的站点外存储：在 Azure Blob 服务上存储备份是一种方便、灵活、易于访问的站点外选项。 为您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份创建站点外存储就像修改您的现有脚本/作业一样简单。 场外存储通常应当远离生产数据库位置，以防止某个灾难可能同时影响场外和生产数据库位置。 通过选择地理复制 Blob 存储区，您在发生可能影响整个区域的灾难时多了一层额外的保护。 此外，备份副本随时随地可用，并可以轻松访问它们来执行还原。  
  
-   备份存档：使用 Azure Blob 存储服务可以更好地替代常用磁带选项来存档备份。 选择磁带存储时可能需要将数据实际运输到场外设施，并且需要采取一些介质保护措施。 在 Azure Blob 存储中存储备份可提供即时、具有高可用性且持久的存档方式。  
  
-   无硬件管理开销： Azure 服务没有硬件管理开销。 Azure 服务可管理硬件并提供异地冗余复制和硬件故障防护。  
  
-   当前，对于在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 虚拟机中运行的实例，可以通过创建附加的磁盘来备份到 azure Blob 存储服务。 不过，你只能将有限数量的磁盘附加到 Azure 虚拟机。 对特大实例的限制为 16 个磁盘；对较小实例的磁盘限制数更少。 通过直接备份到 Azure Blob 存储，你可以绕过 16 个磁盘这一限制。  
  
     此外，存储在 Azure Blob 存储服务中的备份文件直接可用于本地[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure 虚拟机中运行的其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而无需进行数据库附加/分离或者下载和附加 VHD。  
  
-   成本优势：仅对使用的服务付费。 作为场外和备份存档方式可能更加划算。 有关详细信息和链接，请参阅[Azure 计费注意事项](#Billing)部分。  
  
##  <a name="Billing"></a>Azure 计费注意事项：  
 了解 Azure 存储成本使你能够预测在 Azure 中创建和存储备份的成本。  
  
 [Azure 价格计算器](https://go.microsoft.com/fwlink/?LinkId=277060)可以帮助估算你的成本。  
  
 **存储：** 费用基于使用的空间并根据渐变的规模和冗余级别进行计算。 有关详细信息和最新信息，请参阅 **定价详细信息** 文章中的[“数据管理”](https://go.microsoft.com/fwlink/?LinkId=277059) 一节。  
  
 **数据传输：** 向 Azure 的入站数据传输是免费的。 出站传输要支付带宽使用费用，并根据渐变的区域特定标准来计算费用。 有关详细信息，请参阅“定价详细信息”文章中的 [数据传输](https://go.microsoft.com/fwlink/?LinkId=277061) 一节。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 备份到 URL 最佳做法和故障排除](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [备份和还原系统数据库 (SQL Server)](back-up-and-restore-of-system-databases-sql-server.md)   
 [教程： SQL Server 备份和还原到 Azure Blob 存储服务](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server 的 URL 备份](sql-server-backup-to-url.md)  
  
