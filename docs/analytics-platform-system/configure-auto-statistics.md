---
title: 自动统计信息 (Analytics Platform System)
description: 描述分析平台系统 AU7 中引入的自动统计信息功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1c0f4623adad35ab874330b42aa54f6e1b91d961
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550890"
---
# <a name="configure-auto-statistics"></a>配置自动统计信息

了解如何配置并行数据仓库以用于创建和自动更新统计信息的自动统计信息。  利用此功能，可以改进查询计划，并因此提高查询性能。

**适用于：** AP （从 AU7 开始）

## <a name="what-are-statistics"></a>统计信息有哪些？
查询优化统计信息是表的包含有关一个或多个列中的值分布的统计信息的对象。 查询优化器使用这些统计信息来估计基数，或中的行数，查询结果。 这些基数估计启用查询优化器创建高质量查询计划。 例如，在 AP 的基数估计选择随机排列，或复制中较小的和执行此操作对 join 子句中使用的两个表的 MPP 查询优化器使用提高查询性能。  有关详细信息，请参阅[统计信息](../relational-databases/statistics/statistics.md)和[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>自动统计信息有哪些？
自动统计信息是查询优化器创建和自动更新以改进查询计划的统计信息。 统计信息可能会变得过期后加载、 插入、 更新和删除操作。 不自动统计信息的情况下需要执行你自己的分析，以了解哪些列需要统计信息和需要更新统计信息。

自动统计信息包括以下三种设置： 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
在自动创建统计信息选项，AUTO_CREATE_STATISTICS 为 ON，查询优化器将在查询谓词中，根据需要，以改进查询计划的基数估计的单个列上创建统计信息。 这些单列统计信息在现有统计信息对象中尚未具有直方图的列上创建。

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
在自动更新统计信息选项 AUTO_UPDATE_STATISTICS 为 ON 时，查询优化器将确定统计信息何时可能过期，然后在查询使用这些统计信息时更新它们。 统计信息过期后操作插入、 更新、 删除或合并更改表中的数据分布或索引视图。 查询优化器通过计算自最后统计信息更新后数据修改的次数并且将这一修改次数与某一阈值进行比较，确定统计信息何时可能过期。 该阈值基于表中或索引视图中的行数。

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
异步统计信息更新选项 AUTO_UPDATE_STATISTICS_ASYNC 将确定查询优化器是使用同步统计信息更新还是异步统计信息更新。 有关 AP，异步统计信息更新选项为 ON，默认情况下，，并且查询优化器异步更新统计信息。 AUTO_UPDATE_STATISTICS_ASYNC 选项适用于为索引，查询谓词和使用 CREATE STATISTICS 语句创建的统计信息中的单个列创建统计信息对象。

## <a name="configuration-settings-for-system-administrators"></a>系统管理员的配置设置
升级到 AP AU7 后，默认情况下启用了自动统计信息。 系统管理员可以启用或禁用自动统计信息与[功能开关](appliance-feature-switch.md)选项设备配置管理器中。  启用后，用户可以更改每个数据库的统计信息设置。
更改任何功能开关值需要 AP 上的重新启动服务。

## <a name="change-auto-statistics-settings-on-a-database"></a>更改自动在数据库上的统计信息设置
启用自动统计信息后由系统管理员，你可以使用[ALTER DATABASE （并行数据仓库）](/sql/t-sql/statements/alter-database-parallel-data-warehouse)若要更改数据库上的统计信息设置。 如果由系统管理员启用了自动统计信息功能开关，升级到 AU7 之后创建的所有新数据库将具有启用的自动统计信息。 升级到 AU7 之前已存在的所有数据库都有禁用的自动统计信息。 以下示例启用上现有的数据库 myPDW 自动统计信息。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
当 AUTO_UPDATE_STATISTICS 为 ON，AUTO_UPDATE STATISTICS_ASYNC 选项才有效。  因此，统计信息时未更新 AUTO_UPDATE_STATISTICS 为 OFF 和 AUTO_UPDATE_STATISTICS_ASYNC 为 ON。 

### <a name="error-messages"></a>错误消息
你将收到错误消息"此选项不支持 PDW 中"。  当系统管理员尚未启用自动统计信息，并尝试在 ALTER DATABASE 中设置任何自动统计信息选项，将出现此错误。 

### <a name="limitations-and-restrictions"></a>限制和局限
自动统计信息不会对外部表无效。 

### <a name="check-the-current-values"></a>检查当前值
下面的查询返回所有数据库的自动统计信息设置的当前值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

返回值 1 表示将在此设置已打开，并 0 意味着设置处于关闭状态。 

## <a name="next-steps"></a>后续步骤
若要查看你的查询的性能如何，请参阅[监视活动查询](monitoring-active-queries.md)
