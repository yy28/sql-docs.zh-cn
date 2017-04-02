---
title: "暂停跟踪 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "暂停跟踪"
  - "暂时停止跟踪"
  - "跟踪 [SQL Server], 暂停"
  - "停止跟踪"
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# 暂停跟踪 (SQL Server Profiler)
  暂停跟踪可防止捕获更多的事件数据，直到重新启动该跟踪。  
  
 暂停跟踪可以防止捕获事件数据，直到重新启动跟踪。 重新启动跟踪将恢复跟踪操作。 重新启动后以前捕获的数据不会丢失。 重新启动跟踪时，将从启动的那一点恢复数据捕获。 暂停跟踪时，可以更改名称、事件、列和筛选器。 但是不能更改要将跟踪数据发送到的目标和服务器连接。  
  
### 暂停跟踪  
  
1.  选择一个包含正在运行的跟踪的窗口。  
  
2.  在 **“文件”** 菜单上，单击 **“暂停跟踪”**。  
  
## 另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  