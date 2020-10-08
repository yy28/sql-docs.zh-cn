---
title: 启用 SqlClient 中的事件跟踪
description: 介绍如何通过实现事件侦听器来启用 SqlClient 中的事件跟踪以及如何访问事件数据。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725738"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>启用 SqlClient 中的事件跟踪

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[Windows 事件跟踪 (ETW)](/windows/win32/etw/event-tracing-portal) 是一种高效的内核级别跟踪功能，通过此功能，你可以记录驱动程序定义的事件以进行调试和测试。 SqlClient 支持在不同的信息级别捕获 ETW 事件。 若要开始捕获事件跟踪，客户端应用程序应侦听来自 SqlClient 的 EventSource 实现的事件：

```
Microsoft.Data.SqlClient.EventSource
```

当前实现支持以下事件关键字：

| 关键字名称 | 值 | 描述 |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | 启用命令执行前后捕获启动/停止事件。 |
| 跟踪 | 2 | 启用捕获基本应用程序流跟踪事件。 |
| 范围 | 4 | 启用捕获进入和退出事件 |
| NotificationTrace | 8 | 启用捕获 `SqlNotification` 跟踪事件 |
| NotificationScope | 16 | 启用捕获 `SqlNotification` 范围进入和退出事件 |
| PoolerTrace | 32 | 启用捕获连接池流跟踪事件。 |
| PoolerScope | 64 | 启用捕获连接池范围跟踪事件。 |
| AdvancedTrace | 128 | 启用捕获高级流跟踪事件。 |
| AdvancedTraceBin  | 256 | 启用捕获带有其他信息的高级流跟踪事件。 |
| CorrelationTrace | 512 | 启用捕获关联流跟踪事件。 |
| StateDump | 1024 | 启用捕获完整状态转储 `SqlConnection` |
| SNITrace | 2048 | 启用从托管网络实现捕获流跟踪事件（仅适用于 .NET Core） |
| SNIScope | 4096 | 启用从托管网络实现捕获范围事件（仅适用于 .NET Core） |
|||

## <a name="example"></a>示例
下面的示例对“AdventureWorks”示例数据库上的数据操作启用事件跟踪，并在控制台窗口中显示事件。

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="external-resources"></a>外部资源  
有关详细信息，请参阅以下资源。  
  
|资源|说明|  
|--------------|-----------------|  
|[EventSource 类](/dotnet/api/system.diagnostics.tracing.eventsource)|提供用于创建 ETW 事件的功能。| 
|[EventListener 类](/dotnet/api/system.diagnostics.tracing.eventlistener)|提供用于启用和禁用事件源中事件的方法。|