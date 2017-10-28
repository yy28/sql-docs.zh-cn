---
title: "设置作业历史记录日志 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82d09693143af337c03a54e653f029fb50710a17
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
本主题介绍如何设置 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业历史记录日志。  
  
-   **开始之前：**  [安全性](#Security)  
  
-   **若要设置作业历史记录日志，请使用：** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
**设置作业历史记录日志**  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”，然后单击“属性”。  
  
3.  在 **“SQL Server 代理属性”** 对话框中，选择 **“历史记录”** 页。  
  
4.  从下列选项中选择：  
  
    1.  选中 **“限制作业历史记录日志的大小”**，然后键入作业历史记录日志的最大行数和每个作业的最大行数。  
  
    2.  选中 **“自动删除代理历史记录”**，然后指定时间段。这样，早于此时间段的历史记录将从日志中清除。  
  
## <a name="see-also"></a>另请参阅  
[执行作业](../../ssms/agent/implement-jobs.md)  
[监视作业活动](../../ssms/agent/monitor-job-activity.md)  
[创建作业](../../ssms/agent/create-jobs.md)  
  

