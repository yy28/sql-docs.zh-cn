---
title: "监视磁盘使用情况 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据库监视 [SQL Server], 磁盘使用情况"
  - "磁盘 [SQL Server]"
  - "监视性能 [SQL Server], 磁盘使用情况"
  - "服务器性能 [SQL Server], 磁盘使用情况"
  - "监视 [SQL Server], 磁盘活动"
  - "过度换页 [SQL Server]"
  - "优化数据库 [SQL Server], 磁盘使用情况"
  - "I/O [SQL Server], 监视"
  - "磁盘 [SQL Server], 监视活动"
  - "隔离磁盘活动 [SQL Server]"
  - "数据库性能 [SQL Server], 磁盘使用情况"
  - "监视服务器性能 [SQL Server], 磁盘使用情况"
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 监视磁盘使用情况
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Microsoft Windows 操作系统输入/输出 (I/O) 调用来对您的磁盘执行读和写操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理何时以及如何执行磁盘 I/O，但是 Windows 操作系统执行基础 I/O 操作。 I/O 子系统包括系统总线、磁盘控制卡、磁盘、磁带驱动器、CD-ROM 驱动器以及许多其他 I/O 设备。 磁盘 I/O 是导致系统瓶颈的最常见原因。  
  
 监视磁盘活动涉及两个主要方面：  
  
-   监视磁盘 I/O 及检测过度换页  
  
-   隔离 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产生的磁盘活动  
  
 有关详细信息，请参阅 [监视磁盘使用情况](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)。  
  
  