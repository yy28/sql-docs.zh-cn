---
title: 启用或禁用使用情况数据收集和崩溃报告
titleSuffix: Azure Data Studio
description: 本文介绍如何控制如果收集并向 Microsoft 发送使用情况和崩溃报告数据。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: cf358274f3a16f9c4330ad0f093d2ee32ac746b5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783099"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>启用或禁用使用情况数据收集 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>如何禁用遥测数据报告

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 收集使用情况数据并将其发送给 Microsoft，帮助改进我们的产品和服务。 要了解详细信息，请阅读[隐私声明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果你不想要向 Microsoft 发送使用情况数据，则可以设置*telemetry.enableTelemetry*将设置为*false*。

提示中的所有遥测事件[!INCLUDE[name-sos](../includes/name-sos-short.md)]，从**文件** > **首选项** > **设置**，添加以下选项：

```json
    "telemetry.enableTelemetry": false
```

**重要说明**:此选项要求重新启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]才会生效。 

## <a name="how-to-disable-crash-reporting"></a>如何禁用崩溃报告

若要禁用崩溃报告，从**文件** > **首选项** > **设置**，添加以下选项：

```json
    "telemetry.enableCrashReporter": false
```

**重要说明**:此选项要求重新启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]才会生效。

## <a name="additional-resources"></a>其他资源
- [工作区和用户设置](settings.md)
