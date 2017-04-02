---
title: "查看保存的跟踪 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "跟踪 [SQL Server], 查看"
  - "显示跟踪"
  - "查看跟踪"
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# 查看保存的跟踪 (Transact-SQL)
  本主题说明如何使用内置函数查看保存的跟踪。  
  
### 查看特定的跟踪  
  
1.  通过指定需要获得其信息的跟踪的 ID 来执行 **fn_trace_getinfo**。 此函数将返回一个表，表中列出了跟踪、跟踪属性以及有关属性的信息。  
  
     请按以下方式调用此函数：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### 查看所有现有跟踪  
  
1.  通过指定 `0` 或 `default` 来执行 **fn_trace_getinfo**。 此函数将返回一个表，表中列出了所有跟踪、跟踪属性以及有关这些属性的信息。  
  
     请按以下方式调用此函数：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## .NET Framework 安全性  
 若要运行内置函数 **fn_trace_getinfo**，用户需要具有以下权限：  
  
 对服务器具有 ALTER TRACE 权限。  
  
## 另请参阅  
 [sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [使用 SQL Server Profiler 查看和分析跟踪](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  