---
title: "加载服务器容量规划工作表 (SQL Server PDW)"
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
description: "此容量规划工作表可帮助你确定数据加载到 SQL Server PDW 的加载服务器的要求。"
ms.date: 01/05/2017
ms.topic: article
ms.assetid: df2155be-a624-40ba-9a85-58af708f7ce7
caps.latest.revision: "9"
ms.openlocfilehash: 0c5edef2b15b4e8412022e14853ad833cd9bbee5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="loading-server-capacity-planning-worksheet"></a>加载服务器容量规划工作表
此容量规划工作表可帮助你确定数据加载到 SQL Server PDW 的加载服务器的要求。 用于创建您的计划购买或设置现有加载服务器。  
  
## <a name="worksheet-notes"></a>工作表注释
  
1.  此工作表适用于使用的数据将加载的服务器**dwloader**命令行加载工具。  
  
2.  用于加载与 Integration Services 或第三方加载工具的数据，要求可能因而异加载过程中的区别。  
  
3.  大多数要求适用于加载文件，也压缩或未压缩的数据;以粗体显示注明了中要求的任何差异。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪贴板](media/clipboard-icon.png "剪贴板")容量规划工作表  
  
打印此工作表，使用您自己的需求来填充它。  
  
|组件|要求|填充此列中具有自己的要求|建议|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|存储器|你打算在任何给定时间段内加载在服务器上存储的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储要求，找出你打算在任何给定时间段内加载在服务器上存储的数据量。  容量要求适用于仅; 加载文件操作系统和加载文件应存放在不同的磁盘阵列。<br /><br />例如： 如果你打算从磁盘中 3 次每一天，加载 100 GB 的数据而不是每周结束时才会删除数据文件，则你需要最小的 2.1 TB 来存储数据文件。 我们建议在保守和获取有关多 30%存储来满足方差和增长。  对于此示例中，为更好 2.73 TB 的存储空间。|  
|加载速率|每小时的数据加载到 PDW 的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|这是一个估计值。 在计算此要求，则假定的文件已在加载服务器上，而其他加载条件局限于可能。<br /><br />例如： 无需考虑数据可压缩性因为 dwloader 始终发送到 PDW 未压缩的数据。 无需考虑的数据类型转换和目标表的大小。|  
|网络|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|确定你的负载速率要求的最佳网络连接类型。<br /><br />例如： InfiniBand 或 10 Gbit 以太网将提供最佳加载速率。 1 Gbit 以太网将限制负载费率为 360 GB 每小时或更少。|  
|I/O|每小时的读取和写入的字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要加载数据，dwloader 必须的所有数据从磁盘读取发送到 PDW 之前。<br /><br />速度比设备可以从所有加载源接收数据，每个加载服务器无法加载数据。 若要节省资金，规划 I/O 读取加载，以便它不超过设备的负载容量的容量。<br /><br />例如：<br />PDW 接收，并将数据加载到一个 1 机架设备每小时的 1.8 TB 的最大速率。 对于有 2 个或多个机架的装置，最大加载速率是每小时 3.6 TB。<br /><br />如果你打算在同一时间从多个加载服务器加载，每个加载服务器的 I/O 要求将小于一台服务器进行所有加载的时。<br /><br />例如： 一个加载服务器可以加载 1.8 TB 的最多每小时 1 机架设备。 两个加载服务器无法每同时加载 900 GB 每小时到 1 机架设备。 更高的并发级别可以减少效率和最大吞吐量。<br /><br />对于 I/O 容量，考虑所有加载服务器上发生的 I/O。 如果加载服务器的数据负载，如接收数据文件从 ETL 服务器，除了其他输入/输出通信量将增加的 I/O 要求。<br /><br />对于压缩的数据的 I/O 要求取决于数据压缩率。 dwloader 读取压缩的数据，然后发送到 PDW 之前对它进行解压缩。 越高的压缩率、 更少的数据加载服务器将需要从磁盘读取。<br /><br />例如： 如果需要的加载速率为 1.8 TB 每小时，并使用 2:1 的压缩，在加载服务器上存储数据，然后加载服务器需要只应用于每小时从而不是 1.8 TB 的磁盘读取 900 GB。 3:1 的压缩率意味着加载服务器需要每小时从磁盘读取 600 GB。|  
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|用于加载未压缩的数据，dwloader 不是 CPU 密集型应用程序。  作为最低要求，我们建议使用最近制造 2 套接字服务器。<br /><br />用于加载压缩的数据，你需要足够的 CPU 性能，以发送到 PDW 之前解压缩数据。 dwloader 可以同时运行 10 个活动线程。 如果你打算同时加载 10 压缩的文件，我们建议服务器已具有至少 10 核 CPU 或两个 6 核 Cpu。|  
|RAM|加载缓存的文件期间允许 Windows 的内存 GB。|![铅笔图标](media/pencil-icon.png "铅笔图标")|dwloader 加载服务器上使用很少的 RAM。 为性能，Windows 使用内存来阅读它们从磁盘之后缓存加载文件。<br /><br />若要确定对 RAM 的要求，请参阅 Windows Server 安装和任何第三方应用程序的要求。 如果你还没有从其他源的要求，我们建议至少为 32 GB。<br /><br />对于压缩数据，更快的 RAM 很有用，因为它将加快解压缩。|  
  
## <a name="see-also"></a>另请参阅  
[获取和配置加载服务器](acquire-and-configure-loading-server.md)  
[dwloader 命令行加载程序](dwloader.md)  
  
