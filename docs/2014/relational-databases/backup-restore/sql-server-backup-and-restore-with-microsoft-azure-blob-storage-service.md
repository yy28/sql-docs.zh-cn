---
title: SQL Server 备份和还原使用 Windows Azure Blob 存储服务 |Microsoft Docs
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
ms.openlocfilehash: bfc0ef5adeb930988d142a8c4864ff13bcd2964a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064147"
---
# <a name="sql-server-backup-and-restore-with-windows-azure-blob-storage-service"></a>使用 Windows Azure Blob 存储服务进行 SQL Server 备份和还原
  本主题介绍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份和还原从[Windows Azure Blob 存储服务](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。 它还总结了使用 Windows Azure Blob 服务存储 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的好处。  
  
 SQL Server 支持通过以下方式将备份存储到 Windows Azure Blob 存储服务：  
  
-   **管理向 Windows Azure 的备份：** 使用相同的方法用于备份到磁盘和磁带，你现在可备份到 Windows Azure 存储通过指定 URL 作为备份目标。  可使用此功能手动备份或配置自己的备份策略，如同对于本地存储或其他站点外选项所做的一样。 此功能也称为 **SQL Server 备份到 URL**。 有关详细信息，请参阅 [SQL Server Backup to URL](sql-server-backup-to-url.md)。 SQL Server 2012 SP1 CU2 或更高版本中提供此功能。  
  
    > [!NOTE]  
    >  对于版本低于 SQL Server 2014 的 SQL Server，可使用外接程序“SQL Server 备份到 Windows Azure 工具”快速而轻松地向 Windows Azure 存储创建备份。 有关详细信息，请参阅 [下载中心](http://go.microsoft.com/fwlink/?LinkID=324399)。  
  
-   **让 SQL Server 管理向 Windows Azure 备份：** 配置 SQL Server 以管理备份策略和计划备份为单个数据库或多个数据库，或在实例级别设置默认值。 此功能被称为**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**。 有关详细信息请参阅[SQL Server 托管备份到 Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)。 SQL Server 2014 或更高版本中提供此功能。  
  
## <a name="benefits-of-using-the-windows-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>将 Windows Azure Blob 服务用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的好处  
  
-   灵活、可靠、无限制的站点外存储：在 Windows Azure Blob 服务上存储您的备份是一种方便、灵活、易于访问的站点外备选方法。 为您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份创建站点外存储就像修改您的现有脚本/作业一样简单。 站点外存储位置通常应远离生产数据库位置，以防止出现同时影响站点外和生产数据库位置的一个灾难。 通过选择地理复制 Blob 存储区，您在发生可能影响整个区域的灾难时多了一层额外的保护。 此外，备份副本随时随地可用，并可以轻松访问它们来执行还原。  
  
-   备份存档：Windows Azure Blob 存储服务提供替代常用磁带方案的更好的方法来存档备份。 磁带存储可能需要物理传输到站点外设施并采取措施来保护介质。 在 Windows Azure Blob 存储区中存储您的备份可以提供一个即时、高度可用、耐久的存档方案。  
  
-   无硬件管理开销：没有有关 Windows Azure 服务的硬件管理开销。 Windows Azure 服务管理硬件并支持地理复制以提供冗余和防止硬件故障。  
  
-   当前对于在 Windows Azure 虚拟机中运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，可以通过创建附加的磁盘来备份到 Windows Azure Blob 存储服务。 但是，对于可以附加到 Windows Azure 虚拟机的磁盘数有限制。 限制值为：超大实例最多使用 16 个磁盘，较小的实例可使用的磁盘则更少。 通过允许直接备份到 Windows Azure Blob 存储区，您可以绕过 16 个磁盘的限制。  
  
     此外，现在在 Windows Azure Blob 存储服务中存储的备份文件直接可用于内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或在 Windows Azure 虚拟机中运行的另一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不需要进行数据库附加/分离或下载并附加 VHD。  
  
-   成本优势：仅对使用的服务付费。 可以作为经济合算的站点外备份存档方案。 请参阅[Windows Azure 计费注意事项](#Billing)部分，了解详细信息和链接。  
  
##  <a name="Billing"></a> Windows Azure 计费注意事项：  
 了解 Windows Azure 存储成本使您能够预测在 Windows Azure 中创建和存储备份的成本。  
  
 [Windows Azure 定价计算器](http://go.microsoft.com/fwlink/?LinkId=277060)可以帮助估算成本。  
  
 **存储：** 费用基于使用的空间并根据渐变的标准和冗余级别来计算它。 有关详细信息和最新信息，请参阅 **定价详细信息** 文章中的[“数据管理”](http://go.microsoft.com/fwlink/?LinkId=277059) 一节。  
  
 **数据传输：** 入站的数据传输到 Windows Azure 是免费。 出站传输要支付带宽使用费用，并根据渐变的区域特定标准来计算费用。 有关详细信息，请参阅“定价详细信息”文章中的 [数据传输](http://go.microsoft.com/fwlink/?LinkId=277061) 一节。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 备份到 URL 最佳实践和故障排除](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [备份和还原系统数据库 (SQL Server)](back-up-and-restore-of-system-databases-sql-server.md)   
 [教程： SQL Server 备份和还原到 Windows Azure Blob 存储服务](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server 备份到 URL](sql-server-backup-to-url.md)  
  
  
