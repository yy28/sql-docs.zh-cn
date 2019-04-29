---
title: 自动统计信息 (Analytics Platform System)
description: 描述在分析平台系统 AU7 中引入的自动统计信息功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: e48d40d78c25431fd6e5592dacfa410723b31f82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057060"
---
# <a name="configure-auto-statistics"></a>配置自动统计信息

了解如何配置并行数据仓库以用于创建和自动更新统计信息的自动统计信息。  使用此功能以改进查询计划，并因此提高查询性能。

**适用范围：** APS （从 2016 AU7 开始）

## <a name="what-are-statistics"></a>统计信息有哪些？
查询优化统计信息是包含一个或多个表的列中值的分布有关的统计信息的对象。 查询优化器使用这些统计信息来估计基数，或在查询中的行数。 这些基数估计值，允许查询优化器可以创建高质量查询计划。 例如，在 AP，MPP 查询优化器使用基数估计来选择无序播放或复制的两个表和执行此操作对 join 子句中使用较小者提高查询性能。  有关详细信息，请参阅[统计信息](../relational-databases/statistics/statistics.md)和[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>自动统计信息有哪些？
自动统计信息是查询优化器创建并自动更新以改进查询计划的统计信息。 统计信息加载后可能会过期、 插入、 更新和删除操作。 没有自动统计信息，必须执行您自己的分析以了解哪些列需要的统计信息和统计信息需要进行更新。

自动统计信息包括以下三个设置： 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
在自动创建统计信息选项 AUTO_CREATE_STATISTICS 为 ON 时，查询优化器将根据需要在查询谓词中的单独列上创建统计信息，以便改进查询计划的基数估计。 这些单列统计信息在现有统计信息对象中尚未具有直方图的列上创建。

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
在自动更新统计信息选项 AUTO_UPDATE_STATISTICS 为 ON 时，查询优化器将确定统计信息何时可能过期，然后在查询使用这些统计信息时更新它们。 统计信息将在插入、更新、删除或合并操作更改表或索引视图中的数据分布后过期。 查询优化器通过计算自最后统计信息更新后数据修改的次数并且将这一修改次数与某一阈值进行比较，确定统计信息何时可能过期。 该阈值基于表中或索引视图中的行数。

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
异步统计信息更新选项 AUTO_UPDATE_STATISTICS_ASYNC 将确定查询优化器是使用同步统计信息更新还是异步统计信息更新。 有关 APS，默认情况下异步统计信息更新选项为 ON 和查询优化器异步更新统计信息。 AUTO_UPDATE_STATISTICS_ASYNC 选项适用于为索引创建的统计信息对象、查询谓词中的单列以及使用 CREATE STATISTICS 语句创建的统计信息。

## <a name="configuration-settings-for-system-administrators"></a>系统管理员的配置设置
升级到 AP AU7 后，默认情况下启用自动统计信息。 系统管理员可以启用或禁用自动统计信息与[功能开关](appliance-feature-switch.md)选项在设备配置管理器。  启用后，用户可以更改每个数据库的统计信息设置。
更改任何功能开关值需要 AP 上的重新启动服务。

## <a name="change-auto-statistics-settings-on-a-database"></a>更改数据库上的自动统计信息设置
由系统管理员启用自动统计信息后，可以使用[ALTER DATABASE （并行数据仓库）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)若要更改数据库上的统计信息设置。 如果由系统管理员启用自动统计信息功能开关，则升级到 AU7 后创建的任何新数据库将具有启用自动统计信息。 升级到 AU7 之前已存在的所有数据库都有禁用自动统计信息。 以下示例启用现有的数据库 myPDW 的自动统计信息。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
只有 AUTO_UPDATE_STATISTICS 为 ON 时，AUTO_UPDATE STATISTICS_ASYNC 选项仅适用于。  因此，将不更新统计信息 AUTO_UPDATE_STATISTICS 为 OFF 时和 AUTO_UPDATE_STATISTICS_ASYNC 为 ON。 

### <a name="error-messages"></a>错误消息
您可能会收到错误消息"此选项不支持在 PDW 中"。  系统管理员未启用自动统计信息，并尝试在 ALTER DATABASE 设置任何自动统计信息选项时，将发生此错误。 

### <a name="limitations-and-restrictions"></a>限制和局限
自动统计信息不适用于外部表。 

### <a name="check-the-current-values"></a>检查当前值
以下查询返回所有数据库的自动统计信息设置的当前值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

返回值 1 表示在设置上，而 0 表示设置为 off。 

## <a name="next-steps"></a>后续步骤
若要查看如何执行查询，请参阅[监视活动查询](monitoring-active-queries.md)
