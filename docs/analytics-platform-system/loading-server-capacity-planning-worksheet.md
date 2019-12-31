---
title: 正在加载服务器容量规划
description: 此容量计划工作表可帮助你确定加载服务器用于将数据加载到 Analytics 平台系统并行数据仓库的要求。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dded8c79495d0bdc684927f4875a93c3160c1bf
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401035"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>正在加载分析平台系统的服务器容量规划工作表
此容量计划工作表可帮助你确定加载服务器用于将数据加载到 SQL Server PDW 的要求。 使用此功能可以创建用于购买或预配现有加载服务器的计划。  
  
## <a name="worksheet-notes"></a>工作表说明
  
1.  此工作表适用于将通过**dwloader**命令行加载工具加载数据的服务器。  
  
2.  若要使用 Integration Services 或第三方加载工具加载数据，要求可能因加载过程中的不同而有所不同。  
  
3.  大多数要求适用于加载压缩或未压缩的数据文件;要求中的任何差异以粗体显示。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪贴板](media/clipboard-icon.png "剪贴板")容量规划工作表  
  
打印此工作表并根据自己的需求填写。  
  
|组件|要求|根据自己的需求填写此列|建议|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|存储|在任意给定时间段内计划在加载服务器上存储的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储要求，请找出你计划在任何给定时间段在加载服务器上存储的数据量。  容量要求仅适用于加载文件;操作系统和加载文件应位于不同的磁盘阵列上。<br /><br />例如：如果你计划每天3次从磁盘加载 100 GB 数据，但在一周结束之前不删除数据文件，则你需要至少 2.1 TB 存储数据文件。 建议保守，并获得大约30% 的存储空间，以考虑差异和增长。  在此示例中，2.73 TB 的存储空间将更好。|  
|加载速率|要加载到 PDW 中的数据的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|这是一个估计值。 计算此要求时，假定文件已在加载服务器上，并且其他加载条件尽可能好。<br /><br />例如：无需考虑数据 compressibility，因为 dwloader 始终向 PDW 发送未压缩的数据。 无需考虑数据类型转换和目标表的大小。|  
|网络|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|根据负载速率要求确定最佳网络连接类型。<br /><br />例如：无限或 10 Gb 的以太网将提供最佳的加载速度。 1 gb 以太网会将负载速率限制为每小时 360 GB。|  
|I/O|用于读取和写入的每小时字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要加载数据，dwloader 必须先读取磁盘中的所有数据，然后再将其发送到 PDW。<br /><br />每个加载服务器无法更快地加载数据，因为设备可以从所有加载源接收数据。 为了节省资金，请规划 i/o 读取容量以便加载，使其不超过设备的负载容量。<br /><br />例如：<br />PDW 接收数据并将其加载到1机架设备，最大速率为每小时 1.8 TB。 对于具有2个或更多机架的设备，最大负载速率为每小时 3.6 TB。<br /><br />如果你计划同时从多个加载服务器加载，则每个加载服务器的 i/o 要求将小于一个服务器执行所有加载的时间。<br /><br />例如：一个负载服务器最多可为1机架设备每小时加载 1.8 TB。 每个加载服务器每小时可同时加载 900 GB 到1机架设备。 更高的并发级别可以降低效率和最大吞吐量。<br /><br />对于 i/o 容量，请将加载服务器上发生的所有 i/o 都考虑在内。 如果加载服务器除了数据加载之外还有其他 i/o 流量（如从 ETL 服务器接收数据文件），i/o 要求将会增加。<br /><br />对于压缩的数据，i/o 要求取决于数据压缩率。 dwloader 读取压缩的数据，然后在将其发送到 PDW 之前对其 uncompresses。 压缩率越高，加载服务器需要从磁盘读取的数据就越少。<br /><br />例如：如果所需的负载速率为每小时 1.8 TB，并且数据存储在具有2:1 压缩的加载服务器上，则加载服务器只需从磁盘读取 900 GB，而不是从磁盘读取 1.8 TB。 3:1 压缩比意味着加载服务器需要从磁盘读取 600 GB/小时。|  
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|对于加载未压缩的数据，dwloader 不是 CPU 密集型应用程序。  作为最低要求，我们建议使用最近制造的2插槽服务器。<br /><br />若要加载压缩的数据，在将数据发送到 PDW 之前，需要有足够的 CPU 能力来解压缩数据。 dwloader 可以一次运行10个活动线程。 如果你计划同时加载10个压缩文件，则建议服务器至少具有10核 CPU 或两个6核 cpu。|  
|RAM|在加载期间允许 Windows 缓存文件的内存 GB。|![铅笔图标](media/pencil-icon.png "铅笔图标")|dwloader 在加载服务器上使用非常少的 RAM。 为了提高性能，Windows 在从磁盘读取文件后将使用内存来缓存加载文件。<br /><br />若要确定 RAM 要求，请参阅 Windows Server 安装和任何第三方应用程序要求。 如果没有来自其他源的要求，建议至少使用 32 GB。<br /><br />对于压缩的数据，更快的 RAM 非常有用，因为它会提高解压缩速度。|  
  
## <a name="see-also"></a>另请参阅  
[获取和配置加载服务器](acquire-and-configure-loading-server.md)  
[dwloader 命令行加载器](dwloader.md)  
  
