---
title: 备份服务器容量规划的并行数据仓库 |Microsoft Docs
description: 此容量规划工作表可帮助你确定执行并行数据仓库的数据库备份的备份服务器的要求和还原操作。 用于创建您的计划购买新的或预配现有备份服务器。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295062"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>备份服务器容量计划工作的并行数据仓库表
此容量规划工作表可帮助你确定用于执行 SQL Server PDW 的数据库备份的备份服务器的要求和还原操作。 用于创建您的计划购买新的或预配现有备份服务器。  
  
此工作表是对中的说明的补充[获取和配置备份服务器](acquire-and-configure-backup-server.md)。  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>备份服务器的容量规划工作表  

### <a name="notes"></a>说明  
  
1.  此工作表适用于将执行的 PDW 数据库的备份和还原操作的服务器。  
  
2.  备份和还原 PDW 数据库的唯一方法是使用备份数据库和还原数据库 SQL 命令。 但是，在备份服务器上备份数据后，它存在的一系列 Windows 文件。 可以存档的备份文件从服务器到另一个存储位置使用传统 Windows 基于文件的备份方法。  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![剪贴板图标](media/clipboard-icon.png "剪贴板图标")容量规划工作表 
  
打印此工作表并填充您自己的需求。  
  
|组件|要求|在您自己的要求此列中填入|建议|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|存储|计划可以在任何给定时间段内存储备份的服务器上的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储需求，找出你计划在任何给定时间段内存储备份的服务器上的数据量。<br /><br />备份数据存储中以压缩格式的备份服务器上。 数据压缩率取决于你的数据的特征。<br /><br />例如：作为大致的估计，我们建议估计相对于未压缩数据大小 7:1 的压缩率。 这假定至少 80%的数据存储在聚集列存储索引。 例如，如果在数据库中有 700 GB 的未压缩的数据，并且存储在聚集列存储索引，然后你可以估计数据库备份将需要大约 100 GB。<br /><br />如果你计划备份的服务器上具有多个副本的数据库备份，需要对其进行。<br /><br />例如：如果您计划将每个包含 5 TB 未压缩数据的 10 个数据库备份，数据库将具有 50 tb 的数据的组合的大小。 如果你计划备份这些 10 个数据库每天都在一行中的 5 天，未压缩的总大小为 250 TB。 纳入 7:1 的压缩率，你将需要 250 / 7 = 35.7 TB 的存储空间备份服务器上。 我们建议在保守估计，获取有关要考虑的方差并且增长的 30%更多容量。  在此示例中，会更好 46.6 TB。|  
|网络|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|确定可以满足您的负载速率要求的最佳网络连接类型。<br /><br />例如：InfiniBand 或 10Gbit 以太网将提供最佳加载速率。 1Gbit 以太网将限制负载费率为 360 GB 每小时或更少。|  
|I/O|每小时写入的字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|用于将备份写入磁盘，每小时写入速度是最佳的 4 TB。<br /><br />例如：对于可以写入 50 MB/秒的驱动器，你将需要至少 24 个驱动器，还需要更多有关镜像或奇偶校验。<br /><br />对于 I/O 容量，考虑帐户的所有 I/O，加载服务器上发生。 如果加载服务器具有其他除了数据加载，例如从 ETL 服务器接收数据文件的 I/O 流量会增加 I/O 要求。|  
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件不是 CPU 密集型应用程序。  作为最低要求，我们建议使用最近制造双套接字服务器。|  
|RAM|GB 的内存缓存文件期间允许 Windows 将加载。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件需要加载服务器上的很少 RAM。<br /><br />若要确定 RAM 要求，请参阅 Windows Server 安装和任何第三方应用程序要求。 如果您没有从其他源的要求，我们建议至少配置 32gb 内存。|  
  
在完成确定容量要求，请返回到[获取和配置加载服务器](acquire-and-configure-loading-server.md)主题，以制定购买计划。  
  
## <a name="see-also"></a>请参阅  
[备份和加载硬件](backup-and-loading-hardware.md)  
  
