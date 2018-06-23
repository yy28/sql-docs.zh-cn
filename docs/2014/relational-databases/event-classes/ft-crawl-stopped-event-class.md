---
title: FT:Crawl Stopped 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- Crawl Stopped event class
ms.assetid: dbc91bf7-687c-4083-9694-02f3e102c175
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 10fdfc0153cfc9ae71ef1b99bfa5a03d5c7b7f84
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126319"
---
# <a name="ftcrawl-stopped-event-class"></a>FT:Crawl Stopped 事件类
  **:Crawl Stopped** 事件类指示全文爬网（填充）已停止。 之所以停止，可能是由于成功完成了爬网或者出错。  
  
## <a name="ftcrawl-stopped-event-class-data-columns"></a>FT:Crawl Stopped 事件类的数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|已停止全文爬网的数据库的 ID。 可使用 DB_ID 函数来确定数据库的值。|3|是|  
|**EventClass**|**int**|事件类型 = 156。|27|“否”|  
|**EventSequence**|**int**|给定事件在请求中的顺序。|51|“否”|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|是|  
|**Exchange Spill**|**int**|系统分配的对象 ID。 此对象上对全文索引的全文爬网已停止。|22|是|  
|**SessionLoginName**|**nvarchar**|发起会话的用户的登录名。 例如，如果你使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录名。|64|是|  
|**SPID**|**int**|发生该事件的会话的 ID。|12|是|  
|**StartTime**|**datetime**|该事件（如果存在）的启动时间。|14|是|  
|**TransactionID**|**bigint**|系统分配的事务 ID。|4|是|  
  
## <a name="see-also"></a>请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
