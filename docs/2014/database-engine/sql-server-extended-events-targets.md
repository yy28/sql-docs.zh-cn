---
title: SQL Server 扩展事件目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- extended events [SQL Server], targets
ms.assetid: e281684c-40d1-4cf9-a0d4-7ea1ecffa384
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97dbdfcdbc1ddf2a8aba10845f1bc5e3c785a9ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842512"
---
# <a name="sql-server-extended-events-targets"></a>SQL Server Extended Events Targets
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 扩展事件目标是事件使用者。 目标可以写入文件、在内存缓冲区中存储事件数据或聚合事件数据。 目标可以同步或异步处理数据。  
  
 扩展事件的设计确保了对于每个会话都保证目标收到并仅收到一次事件。  
  
 扩展事件提供以下可用于扩展事件会话的目标：  
  
-   [事件计数器](../../2014/database-engine/event-counter-target.md)  
  
     计算在扩展事件会话过程中发生的指定事件的数目。 用于获取有关工作负荷特征的信息，不必因进行完整的事件收集而增加系统开销。 此目标是同步目标。  
  
-   [事件文件](../../2014/database-engine/event-file-target.md)  
  
     用于将事件会话输出从完整内存缓冲区写入磁盘。 此目标是异步目标。  
  
-   [事件配对](../../2014/database-engine/event-pairing-target.md)  
  
     许多类型的事件是成对发生的，例如锁获取和锁释放。 用于确定指定的成对的事件何时未成对发生。 此目标是异步目标。  
  
-   [Windows (ETW) 事件跟踪](../relational-databases/extended-events/event-tracing-for-windows-target.md)  
  
     用于将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 事件与 Windows 操作系统或应用程序事件数据相关联。 此目标是同步目标。  
  
-   [直方图](../../2014/database-engine/histogram-target.md)  
  
     用于基于指定的事件列或操作，对指定事件发生的次数进行计数。 此目标是异步目标。  
  
-   [环形缓冲区](../../2014/database-engine/ring-buffer-target.md)  
  
     用于在先进先出 (FIFO) 的基础上或按事件 FIFO 的基础上将事件数据保存在内存中。 此目标是异步目标。  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../relational-databases/extended-events/extended-events.md)   
 [SQL Server 扩展事件包](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [SQL Server Extended Events Sessions](../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [SQL Server 扩展事件引擎](../relational-databases/extended-events/sql-server-extended-events-engine.md)  
  
  
