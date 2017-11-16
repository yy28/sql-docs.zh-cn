---
title: "查看筛选器信息 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a741b8f1aa4b0095d61c0011518a3f1d855440c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="view-filter-information-transact-sql"></a>查看筛选器信息 (Transact-SQL)
  本主题介绍了如何使用内置函数查看跟踪筛选器信息。  
  
### <a name="to-view-filter-information"></a>查看筛选器信息  
  
1.  通过指定所需筛选器信息的跟踪 ID，执行 **fn_trace_getfilterinfo** 。 此函数将返回一个表，表中列出了筛选器、应用筛选器的列和应用筛选器的值。  
  
     请按以下方式调用此函数：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
