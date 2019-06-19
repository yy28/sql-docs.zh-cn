---
title: 调整作业历史记录日志的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1a8c9ab517d1f6a122144604d6b147e6f5eeaf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650881"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
  本主题说明如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中设置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业历史记录日志的大小限制。  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要设置作业历史记录日志的大小限制，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>基于原始大小调整作业历史记录日志的大小  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”  ，然后单击“属性”  。  
  
3.  选择“历史记录”  页，然后确认已选中“限制作业历史记录日志的大小”  。  
  
4.  在 **“作业历史记录日志的最大大小”** 框中，输入作业历史记录日志允许的最大行数。  
  
5.  在 **“每个作业的最大作业历史记录行数”** 框中，输入作业允许的作业历史记录的最大行数。  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>基于时间调整作业历史记录日志的大小  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”  ，然后单击“属性”  。  
  
3.  选择 **“历史记录”** 页，然后单击 **“自动删除代理历史记录”** 。  
  
4.  选择适当的“天”  、“周”  或“月”  数。  
  
  
