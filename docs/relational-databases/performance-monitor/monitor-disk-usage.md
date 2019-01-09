---
title: 监视磁盘使用情况 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance"
ms.topic: conceptual
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
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: dc8b9edea97ab4a14d3d977e04c9d10e929f8d15
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53379060"
---
# <a name="monitor-disk-usage"></a>监视磁盘使用情况
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Microsoft Windows 操作系统输入/输出 (I/O) 调用来对您的磁盘执行读和写操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理何时以及如何执行磁盘 I/O，但是 Windows 操作系统执行基础 I/O 操作。 I/O 子系统包括系统总线、磁盘控制卡、磁盘、磁带驱动器、CD-ROM 驱动器以及许多其他 I/O 设备。 磁盘 I/O 是导致系统瓶颈的最常见原因。  
  
 监视磁盘活动涉及两个主要方面：  
  
-   监视磁盘 I/O 及检测过度换页  
  
-   隔离 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产生的磁盘活动  
  
 有关详细信息，请参阅 [监视磁盘使用情况](https://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)。  
  
  
