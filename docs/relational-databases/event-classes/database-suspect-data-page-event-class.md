---
title: "Database Suspect Data Page 事件类 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2984420c1a3106b88187af17a9d9babbc106b44b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page 事件类
  **Database Suspect Data Page** 事件类指示何时将某页添加到 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 中的 [suspect_pages](../../relational-databases/databases/msdb-database.md)表中。 在监视是否出现可疑页的跟踪中包括此事件类。  
  
> [!NOTE]  
>  将对应行插入到 **suspect_pages** 表中时，将异步触发此事件。 因此，侦听此事件的作业可能无法立即找到对应的 **suspect_pages** 项。  
  
 如果跟踪中包括 **Database Suspect Data Page** 事件类，则会降低相关开销。 如果可疑页数量增加（例如磁盘驱动器出现问题），则开销可能会增大。  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Database Suspect Data Page 事件类数据列  
  
|数据列名称|数据类型|说明|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|已为其引发可疑页事件的数据库 ID。 这与 **suspect_pages** 表的 **database_id** 列相同。|3|是|  
|**EventClass**|**int**|事件类型为 213。|27|是|  
|**EventSequence**|**int**|事件类在批处理中的顺序。|51|是|  
|**SPID**|**int**|遇到可疑页的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 任务的 ID。|12|是|  
|**StartTime**|**datetime**|事件发生的时间。|14|是|  
|**ObjectID**|**int**|包含可疑页的数据库文件的 ID。 这与 **suspect_pages** 表的 **file_id** 列相同。|22|是|  
|**ObjectID2**|**int**|文件中可疑页的 ID。 这与 **suspect_pages** 表的 **page_id** 列相同。|56|是|  
|**错误**|**int**|遇到的错误的类型。 该值与 **suspect_pages** 表中相应页的 **event_type** 值相同。|31|是|  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [管理 suspect_pages 表 (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
