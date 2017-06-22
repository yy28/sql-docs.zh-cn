---
title: "“数据库”事件类别 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68d15a70be9212c6d19606e8408f1e4ea7bf25df
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="database-event-category"></a>Database 事件类别
  **Database** 事件类别包含用于监视 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的事件类。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[Data File Auto Grow 事件类](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|指示数据文件是自动增长的。 如果数据文件通过 ALTER DATABASE 而显式增长，则不触发此事件。|  
|[Data File Auto Shrink 事件类](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|指示数据文件已收缩。|  
|[数据库镜像连接事件类](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|为报告数据库镜像的传输连接的状态而生成的事件。|  
|[Database Mirroring State Change 事件类](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|指示镜像数据库状态更改的时间。|  
|[Database Suspect Data Page 事件类](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|指示何时将某页添加到 **msdb** 数据库中的 **suspect_pages** 表。|  
|[Log File Auto Grow 事件类](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|指示日志文件是自动增长的。 如果通过 ALTER DATABASE 使日志文件显式增长，则不会触发此事件。|  
|[Log File Auto Shrink 事件类](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|指示日志文件是自动增长的。 如果日志文件通过 ALTER DATABASE 而显式收缩，则不触发此事件。|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
