---
title: 索引磁盘空间示例 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b371198e36cc2e8047ab88275331dab076e0b97b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124323"
---
# <a name="index-disk-space-example"></a>索引磁盘空间示例
  无论什么时候创建、重新生成或删除索引，在相应的文件和文件组中都需要用于存储旧（源）结构和新（目标）结构的磁盘空间。 旧的结构只有在提交索引创建事务后才会释放。 还可能需要附加临时磁盘空间以进行排序操作。 有关详细信息，请参阅 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)。  
  
 在本示例中，将确定创建聚集索引需要的磁盘空间。  
  
 创建聚集索引之前假定满足以下条件：  
  
-   现有表（堆）包含 100 万行。 每行长度为 200 字节。  
  
-   非聚集索引 A 包含 100 万行。 每行长度为 50 字节。  
  
-   非聚集索引 B 包含 100 万行。 每行长度为 80 字节。  
  
-   index create memory 选项设置为 2 MB。  
  
-   所有现有索引和新索引都使用填充因子值 80。 这意味着页的 80% 是满的。  
  
    > [!NOTE]  
    >  由于创建了聚集索引，必须重新生成这两个非聚集索引来用新聚集索引键替换行指示器。  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>脱机索引操作所用的磁盘空间计算  
 在以下步骤中，将计算在索引操作期间使用的临时磁盘空间和用于存储新索引的永久磁盘空间。 显示的计算是近似的；结果将向上舍入而且仅考虑索引叶级别的大小。 代字号 (~) 用来表示近似计算。  
  
1.  确定源结构的大小。  
  
     堆：100 万 * 200 字节 ~ 200 MB  
  
     非聚集索引 A：1 百万 * 50 字节 / 80% ~ 63 MB  
  
     非聚集索引 B：1 百万 * 80 字节 / 80% ~ 100 MB  
  
     现有结构的总大小：363 MB  
  
2.  确定目标索引结构的大小。 假定新聚集键为 24 字节长（包含一个 uniqueifier）。 两个非聚集索引的行指示器（8 字节长）将由此聚集键替换。  
  
     聚集索引：1 百万 * 200 字节 / 80% ~ 250 MB  
  
     非聚集索引 A：1 百万 * (50 – 8 + 24) 字节 / 80% ~ 83 MB  
  
     非聚集索引 B：1 百万 * (80 – 8 + 24) 字节 / 80% ~ 120 MB  
  
     新结构的总大小：453 MB  
  
     索引操作期间支持源结构和目标结构所需的总磁盘空间为 816 MB (363 + 453)。 索引操作提交后将释放当前分配给源结构的空间。  
  
3.  确定用于排序的附加临时磁盘空间。  
  
     将显示在 **tempdb** 中排序所用的空间要求（其中 SORT_IN_TEMPDB 设置为 ON）和在目标位置排序所用的空间要求（其中 SORT_IN_TEMPDB 设置为 OFF）。  
  
    1.  SORT_IN_TEMPDB 设置为 ON 时， **tempdb** 必须有足够磁盘空间以容纳最大的索引（1 百万 * 200 字节 ~ 200 MB）。 在排序操作中没有考虑填充因子。  
  
         **配置 index create memory 服务器配置选项** 值 = 2 MB，附加磁盘空间（在 [tempdb](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 位置）与其相同。  
  
         将 SORT_IN_TEMPDB 设置为 ON 时临时磁盘空间的总大小 ~ 202 MB。  
  
    2.  SORT_IN_TEMPDB 设置为 OFF（默认值）时，步骤 2 中用于新索引的 250 MB 磁盘空间将用于排序。  
  
         [配置 index create memory 服务器配置选项](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 值 = 2 MB，附加磁盘空间（在目标位置）与其相同。  
  
         将 SORT_IN_TEMPDB 设置为 OFF 时临时磁盘空间的总大小 = 2 MB。  
  
 使用 **tempdb**时，将一共需要 1018 MB (816 + 202) 来创建聚集索引和非聚集索引。 虽然使用 **tempdb** 增加了用于创建索引的临时磁盘空间量，但是当 **tempdb** 与用户数据库位于不同的磁盘集上时，它可以减少创建索引所需的时间。 有关使用 **tempdb**的详细信息，请参阅 [用于索引的 SORT_IN_TEMPDB 选项](indexes.md)。  
  
 不使用 **tempdb**时，将一共需要 818 MB (816 + 2) 来创建聚集索引和非聚集索引。  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>联机聚集索引操作所用的磁盘空间计算  
 联机创建、删除或重新生成聚集索引时，将需要附加磁盘空间以生成和维护临时映射索引。 此临时映射索引包含表中每行的一条记录，其内容包含新旧书签列。  
  
 若要计算联机聚集索引操作所需的磁盘空间，请按照脱机索引操作显示的步骤操作并将结果添加到以下步骤的结果中。  
  
-   确定临时映射索引的空间。  
  
     在此示例中，旧书签是堆 （8 字节） 的行 ID (RID)，新书签是聚集键 (24 字节包括`uniqueifier`)。 在新旧书签之间没有重叠的列。  
  
     临时映射索引大小 = 1 百万 * (8 字节 + 24 字节) / 80% ~ 40 MB。  
  
     必须将此磁盘空间添加到目标位置所需磁盘空间（如果 SORT_IN_TEMPDB 设置为 OFF），或添加到 **tempdb** （如果 SORT_IN_TEMPDB 设置为 ON）。  
  
 有关临时映射索引的详细信息，请参阅 [索引 DDL 操作的磁盘空间要求](disk-space-requirements-for-index-ddl-operations.md)。  
  
## <a name="disk-space-summary"></a>磁盘空间摘要  
 下表汇总了磁盘空间计算的结果。  
  
|索引操作|以下结构的位置所需的磁盘空间|  
|---------------------|---------------------------------------------------------------------------|  
|SORT_IN_TEMPDB = ON 时的脱机索引操作|操作期间的总空间： 1018 MB:<br /><br /> - 现有表和索引：363 MB\*<br /><br /> -<br />                    **tempdb**：202 MB*<br /><br /> - 新索引：453 MB<br /><br /> 操作后所需的总空间大小：453 MB|  
|SORT_IN_TEMPDB = OFF 时的脱机索引操作|操作期间的总空间： 816 MB:<br /><br /> - 现有表和索引：363 MB*<br /><br /> - 新索引：453 MB<br /><br /> 操作后所需的总空间大小：453 MB|  
|SORT_IN_TEMPDB = ON 时的联机索引操作|操作期间的总空间： 1058 MB:<br /><br /> - 现有表和索引：363 MB\*<br /><br /> -**tempdb** （包括映射索引）： 242 MB *<br /><br /> - 新索引：453 MB<br /><br /> 操作后所需的总空间大小：453 MB|  
|SORT_IN_TEMPDB = OFF 时的联机索引操作|操作期间的总空间： 856 MB:<br /><br /> - 现有表和索引：363 MB*<br /><br /> - 临时映射索引：40 MB\*<br /><br /> - 新索引：453 MB<br /><br /> 操作后所需的总空间大小：453 MB|  
  
 *索引操作提交后将释放此空间。  
  
 此示例没有考虑任何 **tempdb** 中所需的附加临时磁盘空间（用于存储并发用户更新和删除操作创建的版本记录）。  
  
## <a name="related-content"></a>相关内容  
 [索引 DDL 操作的磁盘空间要求](disk-space-requirements-for-index-ddl-operations.md)  
  
 [索引操作的事务日志磁盘空间](transaction-log-disk-space-for-index-operations.md)  
  
  