---
title: 功能开关 (Analytics Platform System)
description: 有关在分析平台系统 AU7 中引入的两个功能开关的显示信息。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 98a59677267cc2692be7de7e6141e85ec415e61d
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53597054"
---
# <a name="appliance-feature-switches"></a>设备功能开关
**功能开关**页将显示有关分析平台系统 AU7 及更高版本引入了功能开关的信息。 使用此配置页来更新或启用/禁用功能和分析平台系统中的设置。 

> [!NOTE]
> 对功能开关值的更改需要重新启动服务。

![DWConig 设备功能开关](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 设备功能开关") 

## <a name="autostatsenabled"></a>AutoStatsEnabled
控制自动统计信息功能。 此功能开关设置为默认情况下升级到 AU7 之后，则返回 true。 在升级后创建的任何数据库将继承自动创建和异步更新统计信息。 对于现有数据库，数据库管理员可以启用自动统计信息与[ALTER DATABASE （并行数据仓库）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)。 有关统计信息的详细信息，请参阅[统计信息](../relational-databases/statistics/statistics.md)。

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries
可以选取大于 1 的插入/选择操作的 maxdop 设置。 为此设置的选项是 0、 1、 2 和 4 中的，默认值为 1。

##<a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions
在 SQL 查询优化器的公共子表达式的数据移动，从而可以提高查询性能。 可以找到此功能的详细的说明[此处](common-sub-expression-elimination.md)。

## <a name="usecatalogqueries"></a>UseCatalogQueries
使用目录对象，而不是使用 SMO 一些元数据的调用具有显示性能改进。 设置为 true CU7.1，此开关在默认情况下控制该行为。 

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds
控制同步繁忙的系统上，取消涉及数据移动的查询时，数据移动服务 (DMS) 等待的时间。 更新到 AU7 设置此值为 900 秒 （15 分钟） 默认情况下。 有效范围是 0-3600 秒。
