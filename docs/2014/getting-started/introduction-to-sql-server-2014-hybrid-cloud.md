---
title: SQL Server 2014 混合云简介 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89344537c53c4caf066536804557451c965e4596
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241615"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 混合云简介
 大多数应用程序都面临一些重要挑战，如高效率、商业价值、复杂的硬件配置、大量峰值需求以及遵守行业和公司管理规定。 考虑所有这些因素构建企业级技术非常富有挑战性。 Microsoft 混合云策略为传统的私有云、公共云和混合云环境提供支持，从而克服这些重要挑战。 
 
 当你的业务需要时可以按需缩放的灵活 IT 基础结构时，可以构建你的数据中心中的私有云或公有云在 Azure 全球数据中心中。 在扩展数据中心以连接公共云时，您会构建混合云模型。 
 
 本主题介绍支持混合云方案的 SQL Server 2014 功能。 有关 Microsoft 混合云策略和 SQL Server 的详细信息，请参阅 [SQL Server 混合 IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 网站。 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server、 Azure 和混合云 
 使用 Microsoft 技术，您可以在本地和云中运行代码，使用本地数据在云中运行，或者利用多个数据中心完全在云中运行。 因此，您可以自己掌控进度，将您的应用程序移到云中，同时保持现有 IT 投资的价值。 
 
 在本文中，我们将重点包括在本地 SQL Server 和 Azure 公有云产品/服务的混合云方案：[Azure 虚拟机中的 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)并[Azure 存储](http://www.azure.com/documentation/services/storage/)。 具体而言，我们将讨论以下方案： 
 
-  [备份和还原数据库向/从 Azure 存储](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Azure 虚拟机上维护数据库副本](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [在 Azure 存储中存储 SQL Server 数据文件](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [将现有 SQL Server 数据库迁移到 Azure 虚拟机](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>SQL Server 和 Microsoft Azure 的混合云方案 
 
#### <a name="backup"></a> 备份和还原数据库向/从 Azure 存储 
 最基本的管理任务之一是备份和还原数据库。 使用 SQL Server 和 Azure，你可以安全地备份在云中的数据库。 
 
 使用 SQL Server 的备份和还原功能与 Azure 存储作为备份目标的主要优点包括： 
 
-  无限制的低成本存储 
 
-  高度可用的存储（地理复制确保无数据丢失） 
 
-  可支持灾难恢复和合规性要求的站点外存储 
 
-  简化的远程备份和还原过程 
 
 下面是针对云和本地方案的 SQL Server 备份和还原功能列表： 
 
-  [SQL Server 备份到 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)功能，可通过指定 URL 作为备份目标备份到 Azure 存储。 使用此功能，您可以执行手动备份或配置自己的备份策略，就像对本地存储或其他站点外选项所做的一样。 
 
-  [备份加密](../relational-databases/backup-restore/backup-encryption.md)功能，可创建在为存储目标备份时加密数据： 在本地和 Azure 存储。 
 
-  [备份压缩 (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md)功能，可创建一个备份，该值小于相同数据的未压缩的备份。 压缩备份需要较少设备 I/O，因此通常会显著提高备份速度。 在 Azure 存储中存储备份文件时，这可以带来很多好处。 
 
-  [SQL Server 托管备份到 Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx)功能，您可以将 SQL Server 数据库自动备份到[Azure 存储](http://www.azure.com/documentation/services/storage/)。 使用此功能，您可以配置 SQL Server 以管理备份策略和为一个数据库或多个数据库安排备份，或在实例级别设置默认值。 
 
-  [SQL Server 备份到 Azure 工具](https://www.microsoft.com/download/details.aspx?id=40740)可将数据备份到 Azure Blob 存储，可以加密和压缩存储在本地或云中的 SQL Server 备份。 通过此工具可以对多个版本的 SQL Server（如 SQL Server 2005、2008、2008 R2 和 2014）使用单个云备份策略。 
 
#### <a name="replica"></a> Azure 虚拟机上维护数据库副本 
 将数据库某个稳定的灾难恢复解决方案对于业务的成功至关重要。 大多数客户需要配置灾难恢复站点和购买其他硬件来制作数据库副本。 使用 SQL Server 和 Azure，可以维护在云中将数据库的一个或多个副本。 
 
 Azure 中维护辅助副本的主要优点包括： 
 
-  低成本灾难恢复解决方案 
 
-  透明应用程序故障转移 
 
-  转移读取工作负荷和备份的可用副本 
 
 您可以使用任何以下方法维护 Azure 中的次要副本： 
 
-  [添加 Azure 副本向导](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx)，可将数据库的一个或多个副本部署到 Azure 中用于灾难恢复的虚拟机。 
 
-  AlwaysOn 可用性组、 数据库镜像和日志传送可用于解决应用程序的高可用性和灾难恢复需求的最常见技术。 有关信息，请参阅[高可用性和灾难恢复的 Azure 虚拟机中 SQL Server](https://msdn.microsoft.com/library/azure/jj870962.aspx)。 
 
#### <a name="store"></a> 在 Azure 存储中存储 SQL Server 数据文件 
 在 Azure 存储中存储的本地 SQL Server 数据文件为数据库提供灵活、 可靠和无限制的站外存储。 从 SQL Server 2014 开始，你可以使用[Miceosoft Azure 中的 SQL Server 数据文件](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure)将 SQL Server 数据库文件存储在 Azure 存储中。 使用此功能，您可以将数据和日志文件从本地数据库到 Azure 存储，同时保留在本地运行的 SQL Server 的计算节点。 此功能使你能够在 Azure 存储中不受限制的存储容量。 
 
 存储 SQL Server 数据文件 Azure 存储的主要优点包括： 
 
-  在 Azure 存储中的无限制的低成本存储 
 
-  最适合用于将历史数据读取工作负荷转移到云中以支持本地报表应用程序 
 
-  通过分离计算实例（SQL Server 实例）和数据（SQL Server 数据文件）简化灾难恢复。 这使您轻松地将该数据库附加到另一个实例的 SQL Server 的本地环境中或在发生灾难时的 Azure 虚拟机中。 
 
#### <a name="migrate"></a> 将现有 SQL Server 数据库迁移到 Azure 虚拟机 
 对企业而言，云计算具备一些重要优势，如按使用付费的无限虚拟资源，您可以利用公共可用的云数据中心而不是自己构建和管理数据中心，从而降低 IT 和硬件成本。 
 
 与[Azure 虚拟机中 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)，你可以将现有的本地应用程序到 Azure 且需要最少或不更改代码。 管理员和开发人员仍然可以使用本地可用的开发和管理工具。 
 
 将数据库从本地 SQL Server 移到 SQL Server Azure 虚拟机中运行通常采用以下方式之一： 
 
-  **仅移动数据库：** 有几个工具和技术可用于将现有的本地数据库移到 Azure 虚拟机中 SQL Server。 有关指导原则和建议迁移到 Azure 虚拟机中 SQL Server，请参阅[准备迁移到 Azure 虚拟机中 SQL Server](https://msdn.microsoft.com/library/dn133142.aspx)以及[迁移到 Azure 虚拟机中 SQL Server](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   此外，从 SQL Server 2014，新向导，开始[将 SQL Server 数据库部署到 Microsoft Azure 虚拟机](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)可供您将数据库部署到 Azure 虚拟机中运行的另一个 SQL Server 实例。 
 
-  **移动整个虚拟机：** 可以将 SQL Server 虚拟机放入 Azure，也可以使用平台映像创建一个。 然后，您可以将已经包含数据的数据磁盘上载并附加到虚拟机或向虚拟机附加空磁盘。 数据文件和应用程序数据的附加的数据磁盘在 Azure 虚拟机上有 SQL Server 数据实例提供一个永久性存储。 有关全面的信息和操作指南，请参阅[SQL Server 部署在 Azure 虚拟机](https://msdn.microsoft.com/library/dn133141.aspx)。 
 
 如果你打算将应用程序层 （如表示层、 业务层和数据库层） 移到 Azure 虚拟机，我们建议您查看中提供的建议[应用程序模式和开发适用于 Azure 虚拟机中 SQL Server 策略](https://msdn.microsoft.com/library/dn574746.aspx)一文。 本文的目的是为解决方案架构师和开发人员奠定了良好的应用程序体系结构和设计，它们可以按照迁移到 Azure 以及开发新应用程序在 Azure 中的现有应用程序时。 对于每个应用程序模式，这篇文章都介绍了一个本地方案、相应的云解决方案以及相关的技术建议。 此外，本文讨论 Azure 特定开发策略，以便可以正确设计应用程序。 
 
## <a name="see-also"></a>另请参阅 
 [SQL Server 2014 CTP2 产品指南](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server 混合云博客系列](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [迁移到 Azure 数据中心的应用程序](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
 
