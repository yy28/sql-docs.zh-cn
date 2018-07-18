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
ms.openlocfilehash: b06c715549cd1c9cf464a13b03790764ebf40b97
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107175"
---
#<a name="appliance-feature-switch"></a>设备功能开关
**功能开关**页将显示有关引入了两个功能开关的信息在分析平台系统 2016年-AU7。 使用此页可以更新或启用/禁用功能和分析平台系统中的设置。 更改功能切换值需要重新启动服务。

![DWConig 设备功能开关](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 设备功能开关") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 开关
控制自动统计信息功能。 此功能开关设置为默认情况下升级到 AU7 之后，则返回 true。 在升级后创建的任何数据库将继承自动创建和异步更新统计信息。 对于现有数据库，数据库管理员可以启用自动统计信息与 [更改数据库] （/ sql/t-sql/statements/alter-database-parallel-data-warehouse）。 有关统计信息的详细信息，请参阅[统计信息](../relational-databases/statistics/statistics.md)。

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 开关
控制数据移动服务 (DMS) 同步繁忙的系统上，在涉及数据移动的查询被取消，等待的时间。 更新到 AU7 设置此值为 900 秒 （15 分钟） 默认情况下。 有效范围是 0 – 3600 秒。
