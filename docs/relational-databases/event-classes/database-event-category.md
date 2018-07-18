---
title: “数据库”事件类别 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e5e7163438232987bc15cd655612da23653d6e59
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326338"
---
# <a name="database-event-category"></a>Database 事件类别
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Database** 事件类别包含用于监视 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的事件类。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
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
  
  
