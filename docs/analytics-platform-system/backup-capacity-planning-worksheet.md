---
title: 备份服务器容量规划工作表 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 此容量规划工作表可帮助你确定执行 SQL Server PDW 数据库备份的备份服务器的要求和还原操作。
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: 6
ms.openlocfilehash: 1548d284f78043e5f878bafe9922480fe762dbfe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="backup-server-capacity-planning-worksheet"></a>备份服务器容量规划工作表
此容量规划工作表可帮助你确定执行 SQL Server PDW 数据库备份的备份服务器的要求和还原操作。 用于创建您的计划购买新的或设置现有备份服务器。  
  
此工作表是对中的说明的补充[获取和配置备份服务器](acquire-and-configure-backup-server.md)。  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>备份服务器的容量规划工作表  

### <a name="notes"></a>说明  
  
1.  此工作表适用于将执行对 PDW 数据库的备份和还原操作的服务器。  
  
2.  备份和还原 PDW 数据库的唯一方法是使用备份数据库和还原数据库 SQL 命令。 但是，在备份服务器上备份数据后，它作为存在一组 Windows 文件。 你可以将从你的服务器备份文件存档到另一个存储位置，通过使用传统 Windows 基于文件的备份方法。  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![剪贴板图标](media/clipboard-icon.png "剪贴板图标")容量规划工作表 
  
打印此工作表，使用您自己的需求来填充它。  
  
|组件|要求|填充此列中具有自己的要求|建议|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|存储器|你打算在任何给定时间段内存储备份的服务器上的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储要求，找出你打算在任何给定时间段内存储备份的服务器上的数据量。<br /><br />备份数据存储在备份服务器以压缩格式。 数据压缩率取决于你的数据的特征。<br /><br />例如： 作为粗略估计，我们建议估计相对于你未压缩的数据大小 7:1 的压缩率。 这假定至少 80%的数据存储在聚集列存储索引。 例如，如果在数据库中具有 700 GB 的未压缩的数据，并且它存储在聚集列存储索引，然后你可以估计数据库备份将需要约 100 GB。<br /><br />如果你计划在备份服务器上拥有多个副本的数据库备份，你需要考虑这些区域。<br /><br />例如： 如果您计划用于备份，每个包含 5 TB 的未压缩的数据的 10 个数据库，数据库具有的组合的大小为 50 tb 的数据。 如果你打算在一行中的 5 天备份这些 10 个数据库每天，总的未压缩的大小是 250 TB。 7:1 的压缩比将分离后，你将需要 250 / 7 = 35.7 TB 的备份服务器上的存储。 我们建议在保守和获取有关 30%的更多容量来应对方差和增长。  在此示例中，将更好 46.6 TB。|  
|Network|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|确定最佳的网络连接类型可以满足负载速率要求。<br /><br />例如： InfiniBand 或 10Gbit 以太网将提供最优加载速率。 1Gbit 以太网将限制负载费率为 360 GB 每小时或更少。|  
|I/O|每小时写入的字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|用于写入到磁盘，每小时写入速度是最佳的 4 TB 的备份。<br /><br />例如： 对于可以写入 50 MB/秒，您将需要至少 24 驱动器的驱动器，加上更高，镜像或奇偶校验。<br /><br />对于 I/O 容量，考虑所有加载服务器上发生的 I/O。 如果加载服务器的数据负载，如接收数据文件从 ETL 服务器，除了其他输入/输出通信量将增加的 I/O 要求。|  
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件不是 CPU 密集型应用程序。  作为最低要求，我们建议使用最近制造 2 套接字服务器。|  
|RAM|加载缓存的文件期间允许 Windows 的内存 GB。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件需要很少加载服务器上的 RAM。<br /><br />若要确定对 RAM 的要求，请参阅 Windows Server 安装和任何第三方应用程序的要求。 如果你还没有从其他源的要求，我们建议至少为 32 GB。|  
  
在完成确定你的容量要求，请返回到[获取和配置加载服务器](acquire-and-configure-loading-server.md)计划购买的主题。  
  
## <a name="see-also"></a>另请参阅  
[备份和加载硬件](backup-and-loading-hardware.md)  
  
