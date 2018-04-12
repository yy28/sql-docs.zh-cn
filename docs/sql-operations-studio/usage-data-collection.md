---
title: 启用或禁用使用情况数据收集和崩溃报告 SQL Operations Studio (preview) |Microsoft 文档
description: 此文章介绍了如何控制如果使用情况和崩溃报告数据收集和发送给 Microsoft。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae620951028ba8e0e82f89c4251238c92bc614ca
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>启用或禁用使用情况数据收集[!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>如何禁用遥测报告

[!INCLUDE[name-sos](../includes/name-sos-short.md)]收集使用情况数据，并将其发送给 Microsoft，帮助改进我们的产品和服务。 要了解详细信息，请阅读[隐私声明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果你不想要向 Microsoft 发送使用情况数据，则可以设置*telemetry.enableTelemetry*将设置为*false*。

若要抑制中的所有遥测事件[!INCLUDE[name-sos](../includes/name-sos-short.md)]，从**文件** > **首选项** > **设置**，添加以下选项：

```json
    "telemetry.enableTelemetry": false
```

**重要说明**： 此选项，需要重新启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]才会生效。 

## <a name="how-to-disable-crash-reporting"></a>如何禁用崩溃报告

若要禁用崩溃报告，从**文件** > **首选项** > **设置**，添加以下选项：

```json
    "telemetry.enableCrashReporter": false
```

**重要说明**： 此选项，需要重新启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]才会生效。

## <a name="additional-resources"></a>其他资源
- [工作区和用户设置](settings.md)