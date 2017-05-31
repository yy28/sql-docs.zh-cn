---
title: "监视磁盘使用情况 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ff4acc6d6465b09c721d376b14ba6574938ef38
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="monitor-disk-usage"></a>监视磁盘使用情况
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Microsoft Windows 操作系统输入/输出 (I/O) 调用来对您的磁盘执行读和写操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理何时以及如何执行磁盘 I/O，但是 Windows 操作系统执行基础 I/O 操作。 I/O 子系统包括系统总线、磁盘控制卡、磁盘、磁带驱动器、CD-ROM 驱动器以及许多其他 I/O 设备。 磁盘 I/O 是导致系统瓶颈的最常见原因。  
  
 监视磁盘活动涉及两个主要方面：  
  
-   监视磁盘 I/O 及检测过度换页  
  
-   隔离 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产生的磁盘活动  
  
 有关详细信息，请参阅 [监视磁盘使用情况](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)。  
  
  
