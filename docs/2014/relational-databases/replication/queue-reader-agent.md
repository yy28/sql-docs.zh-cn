---
title: 队列读取器代理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f07c9be82be63d01d563499a80e049e572a4150
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63262062"
---
# <a name="queue-reader-agent"></a>队列读取器代理
  **“队列读取器代理”** 对话框显示有关队列读取器代理的详细信息，包括状态、历史记录、信息性消息和所有错误消息。  
  
## <a name="options"></a>选项  
 从 **“视图”** 菜单中选择要查看的队列读取器代理会话，然后在标记为 **“队列读取器代理的会话”** 的网格中选择特定的会话。 有关此会话的详细信息显示在标记为 **“所选会话中的操作”** 的网格中。 如果所选会话由于出错而结束，则还将显示一个标记为 **“所选会话的错误详细信息或消息”** 的文本区域。  
  
 **视图**  
 选择要查看的队列读取器代理会话。 队列读取器代理通常连续运行，因此可能只有一个可供查看的会话。  
  
 **Status**  
 队列读取器代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   正在重试失败的命令  
  
-   未运行  
  
-   正在运行  
  
 **Start Time**  
 会话的开始时间。  
  
 **结束时间**  
 会话的结束时间。 如果代理尚未停止，此字段为空。  
  
 **Duration**  
 队列读取器代理已在此会话中运行的时间。 如果代理当前正在运行，该时间表示已用时间；如果代理会话已经结束，则该时间表示会话的总时间。  
  
 **错误消息**  
 如果会话由于出错而结束，此字段将显示队列读取器代理记录的上一条错误消息。 如果某会话未因出错而结束，此字段为空白。  
  
 **操作消息**  
 队列读取器代理在所选会话期间记录的所有信息性消息和错误消息。  
  
 **操作时间**  
 执行 **“操作消息”** 列中所述操作的时间。  
  
 **“所选会话的错误详细信息或消息”**  
 只有当所选会话在 **“状态”** 列中显示 **“错误”** 值时，才会显示此项。 此文本区域显示详细错误信息以及出错时尝试执行的命令。 另外，还包括指向与该错误相关的其他内容的链接。  
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [使用复制监视器查看信息和执行任务](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [监视复制](monitoring-replication.md)   
 [复制代理概述](agents/replication-agents-overview.md)  
  
  
