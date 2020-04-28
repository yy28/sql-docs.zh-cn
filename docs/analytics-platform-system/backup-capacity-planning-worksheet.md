---
title: 备份服务器容量规划
description: 此容量计划工作表可帮助您确定备份服务器执行并行数据仓库数据库备份和还原操作的要求。 使用此功能可以创建计划，以购买新的或预配现有备份服务器。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 57b036269dd4aeed91cf8af811bd2f24faecbb98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78171606"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>备份服务器容量规划工作表-并行数据仓库
此容量计划工作表可帮助您确定备份服务器执行 SQL Server PDW 数据库备份和还原操作的要求。 使用此功能可以创建计划，以购买新的或预配现有备份服务器。

此工作表是对[获取和配置备份服务器](acquire-and-configure-backup-server.md)中的说明的补充。

## <a name="capacity-planning-worksheet-for-backup-servers"></a>备份服务器的容量规划工作表

### <a name="notes"></a>说明

1.  此工作表适用于将对 PDW 数据库执行备份和还原操作的服务器。

2.  备份和还原 PDW 数据库的唯一方法是使用备份数据库和还原数据库 SQL 命令。 但是，一旦备份数据位于备份服务器上，它就会作为一组 Windows 文件存在。 你可以通过使用传统的基于 Windows 文件的备份方法将备份文件从服务器存档到另一个存储位置。

### <a name="clipboard-icon-capacity-planning-worksheet"></a>![剪贴板图标](media/clipboard-icon.png "剪贴板图标")容量规划工作表 

打印此工作表并根据自己的需求填写。

|组件|要求|根据自己的需求填写此列|建议|
|-------------|---------------|--------------------------------------------------|-------------------|
|存储|你计划在任何给定时间段在备份服务器上存储的最大字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要确定存储要求，请找出你计划在任何给定时间段在备份服务器上存储的数据量。<br /><br />备份数据以压缩格式存储在备份服务器上。 数据压缩率取决于数据的特征。<br /><br />例如：作为粗略估算，建议相对于未压缩数据的大小估计7:1 的压缩率。 这假设至少80% 的数据存储在聚集列存储索引中。 例如，如果数据库中的未压缩数据量为 700 GB，并将其存储在聚集列存储索引中，则可以估计数据库备份需要大约 100 GB。<br /><br />如果你计划在备份服务器上具有数据库备份的多个副本，则需要考虑它们。<br /><br />例如：如果计划备份10个数据库，每个数据库都包含 5 TB 未压缩的数据，则数据库的总大小为 50 TB。 如果计划在每天的5天内备份这10个数据库，则未压缩的总大小为 250 TB。 采用7:1 压缩比，你将需要备份服务器上的 250/7 = 35.7 TB 的存储空间。 建议保守，并获得约30% 的额外容量来考虑差异和增长。  在此示例中，46.6 TB 将更好。|
|网络|网络连接类型。|![铅笔图标](media/pencil-icon.png "铅笔图标")|确定可满足负载速率要求的最佳网络连接类型。<br /><br />例如： "10Gbit" 或 " 1Gbit 以太网会将负载速率限制为每小时 360 GB。|
|I/O|写入的每小时字节数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|若要将备份写入磁盘，每小时 4 TB 写入速度都是最佳的。<br /><br />例如：对于可以写入 50 MB/秒的驱动器，你将需要至少24个驱动器，另外还需要更多的镜像或奇偶校验。<br /><br />对于 i/o 容量，请将加载服务器上发生的所有 i/o 都考虑在内。 如果加载服务器除了数据加载之外还有其他 i/o 流量（如从 ETL 服务器接收数据文件），i/o 要求将会增加。|
|CPU|插槽数。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件不是 CPU 密集型应用程序。  作为最低要求，我们建议使用最近制造的2插槽服务器。|
|RAM|在加载期间允许 Windows 缓存文件的内存 GB。|![铅笔图标](media/pencil-icon.png "铅笔图标")|接收和存储备份文件在加载服务器上需要的 RAM 非常少。<br /><br />若要确定 RAM 要求，请参阅 Windows Server 安装和任何第三方应用程序要求。 如果没有来自其他源的要求，建议至少使用 32 GB。|

确定容量需求后，返回到 "[获取并配置加载服务器](acquire-and-configure-loading-server.md)" 主题来计划购买。

## <a name="see-also"></a>另请参阅
[备份和加载硬件](backup-and-loading-hardware.md)

