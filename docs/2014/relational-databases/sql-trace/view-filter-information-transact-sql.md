---
title: 查看筛选器信息 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f6a69932f4a98561f7bfa203abcc990d12e0d84
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220483"
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
  
## <a name="see-also"></a>请参阅  
 [sys.fn_trace_getfilterinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)   
 [系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
