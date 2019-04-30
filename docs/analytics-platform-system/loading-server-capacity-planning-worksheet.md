---
title: 正在加载服务器容量规划的分析平台系统 |Microsoft Docs
description: 此容量规划工作表可帮助您确定用于将数据加载到分析平台系统并行数据仓库的加载服务器的要求。"
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f0efd7e0688496d5af7887431ca00ae683c874f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213391"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>为分析平台系统加载服务器容量规划工作表
此容量规划工作表可帮助您确定数据加载到 SQL Server PDW 加载服务器的要求。 用于创建您的计划购买或预配现有的加载服务器。  
  
## <a name="worksheet-notes"></a>工作表注释
  
1.  此工作表适用于使用的数据将加载的服务器**dwloader**命令行加载工具。  
  
2.  有关加载数据使用 Integration Services 或第三方加载工具，要求可以根据在加载过程中的差异可能有所不同。  
  
3.  大多数要求应用于加载任一压缩或未压缩数据文件;以粗体显示注明了要求存在差异。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪贴板](media/clipboard-icon.png "剪贴板")容量规划工作表  
  
打印此工作表并填充您自己的需求。  
  
|组件|要求|在您自己的要求此列中填入|建议|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|存储|计划可以在任何给定时间段内加载服务器上存储的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储需求，找出你计划在任何给定时间段内加载服务器上存储的数据量。  容量需求是负载仅对文件;操作系统和负载文件应位于不同磁盘阵列。<br /><br />例如：如果你计划从磁盘 3 次加载 100 GB 数据的每一天，但不是删除数据文件的一周，则结束时才需要最小的 2.1 TB 用于存储数据文件。 我们建议在保守估计，获取有关 30%的存储帐户的方差和增长。  此示例中，会更好 2.73 TB 的存储空间。|  
|加载速率|每小时的数据加载到 PDW 的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|这是一个估计值。 计算此要求后，假定文件已在加载服务器上，但其他加载条件不局限于可能。<br /><br />例如：无需考虑的数据可压缩性由于 dwloader 始终发送未压缩到 PDW 数据。 无需考虑的数据类型转换和目标表的大小。|  
|网络|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|确定您的负载速率要求的最佳网络连接类型。<br /><br />例如：InfiniBand 或 10 千兆位以太网将提供最佳加载速率。 1 千兆位以太网将限制负载费率为 360 GB 每小时或更少。|  
|I/O|每小时针对读取和写入字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要加载数据，dwloader 必须的所有数据从磁盘读取发送到 PDW 之前。<br /><br />每个加载服务器不能比设备能够接收来自所有加载源的数据更快地加载数据。 若要节省资金，计划的 I/O 读取用于加载，使其不超过设备的负载容量的容量。<br /><br />例如：<br />PDW 接收，并将数据加载到的最大速度的 1.8 TB 为千瓦时，一个 1 机架设备。 对于有 2 个或多个机架的装置，最大加载速率为每小时 3.6 TB。<br /><br />如果你打算在同一时间从多个加载服务器加载，加载的每个服务器的 I/O 要求将小于一台服务器在执行时所有加载。<br /><br />例如：一个加载服务器可以加载每小时 1 机架设备最多为 1.8 TB。 两个加载服务器可能每个同时加载 900 GB 每小时到 1 机架设备。 更高级别的并发性可以减少效率和最大吞吐量。<br /><br />对于 I/O 容量，考虑帐户的所有 I/O，加载服务器上发生。 如果加载服务器具有其他除了数据加载，例如从 ETL 服务器接收数据文件的 I/O 流量会增加 I/O 要求。<br /><br />有关压缩数据的 I/O 要求取决于数据压缩率。 dwloader 读取压缩的数据，然后将其发送到 PDW 之前将它解压缩。 更高级的压缩率、 较少的数据加载服务器将需要从磁盘读取。<br /><br />例如：如果需要的加载速率是每小时、 1.8 TB 的数据存储压缩率 2:1 加载服务器上，然后加载服务器只需每小时从而不是 1.8 TB 的磁盘读取的 900 GB。 3:1 的压缩率意味着加载服务器需要每小时从磁盘读取的 600 GB。|  
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|有关加载的未压缩的数据，dwloader 不占用 CPU 的应用程序。  作为最低要求，我们建议使用最近制造双套接字服务器。<br /><br />对于加载压缩的数据，您需要足够的 CPU 能力，将其发送到 PDW 之前解压缩数据。 dwloader 可以同时运行 10 个活动线程。 如果你计划同时加载 10 个压缩的文件，我们建议在服务器具有至少一个 10 核心的 CPU 或两个 6 核 Cpu。|  
|RAM|GB 的内存缓存文件期间允许 Windows 将加载。|![铅笔图标](media/pencil-icon.png "铅笔图标")|dwloader 加载服务器上使用很少的 RAM。 为性能，Windows 使用内存来缓存读取后，从磁盘加载文件。<br /><br />若要确定 RAM 要求，请参阅 Windows Server 安装和任何第三方应用程序要求。 如果您没有从其他源的要求，我们建议至少配置 32gb 内存。<br /><br />对于压缩的数据，更快的 RAM 非常有用，因为这将加快解压缩。|  
  
## <a name="see-also"></a>请参阅  
[获取和配置加载服务器](acquire-and-configure-loading-server.md)  
[dwloader 命令行加载程序](dwloader.md)  
  
