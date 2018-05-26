---
title: 功能开关 (Analytics Platform System)
description: 显示有关分析平台系统 AU7 中引入的两个功能开关的信息。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e384a252584fed0e7543a7a4000fc9a70f6533e7
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
---
#<a name="appliance-feature-switch"></a>设备功能开关
**功能开关**页中分析平台系统 AU7 显示有关这两个功能开关引入的信息。 使用此页可以更新或启用/禁用功能和分析平台系统中的设置。 更改交换机特征值需要重新启动服务。

![DWConig 设备功能开关](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 设备功能开关") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 交换机
控制自动统计信息功能。 此功能开关设置为 true 默认情况下，在升级到 AU7 之后。 在升级后创建的任何数据库将继承自动创建和异步更新统计信息。 对于现有数据库，数据库管理员可以启用自动统计信息 [更改数据库] （/ sql/t-sql/statements/alter-database-parallel-data-warehouse）。 有关统计信息的详细信息，请参阅[统计信息](../relational-databases/statistics/statistics.md)。

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 交换机
控制数据移动服务 (DMS) 同步在繁忙的系统，在涉及数据移动的查询被取消，等待的时间。 更新到 AU7 将设置此值为 900 秒 （15 分钟） 默认情况下。 有效范围为 0 – 3600 秒。
