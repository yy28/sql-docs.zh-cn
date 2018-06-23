---
title: 查看保存的跟踪 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f417eb54eff29631f4a24ebbf48de40937a50c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016782"
---
# <a name="view-a-saved-trace-transact-sql"></a>查看保存的跟踪 (Transact-SQL)
  本主题说明如何使用内置函数查看保存的跟踪。  
  
### <a name="to-view-a-specific-trace"></a>查看特定的跟踪  
  
1.  通过指定需要获得其信息的跟踪的 ID 来执行 **fn_trace_getinfo** 。 此函数将返回一个表，表中列出了跟踪、跟踪属性以及有关属性的信息。  
  
     请按以下方式调用此函数：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>查看所有现有跟踪  
  
1.  通过指定 **或** 来执行 `0` fn_trace_getinfo `default`。 此函数将返回一个表，表中列出了所有跟踪、跟踪属性以及有关这些属性的信息。  
  
     请按以下方式调用此函数：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 若要运行内置函数 **fn_trace_getinfo**，用户需要具有以下权限：  
  
 对服务器具有 ALTER TRACE 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.fn_trace_getinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [使用 SQL Server Profiler 查看和分析跟踪](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
