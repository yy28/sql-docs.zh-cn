---
title: 查看保存的跟踪 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16adeb7225df27d571e3c8ea30daa44151f3c19c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63285581"
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
  
## <a name="see-also"></a>另请参阅  
 [sys.fn_trace_getinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [使用 SQL Server Profiler 查看和分析跟踪](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
