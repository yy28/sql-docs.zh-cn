---
title: 运行复制维护作业 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4b6f48a679463d258756142a81ea87dcc10d455c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124308"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>执行复制维护作业 (SQL Server Management Studio)
  复制使用下列维护作业：  
  
-   **重新初始化数据验证失败的订阅**  
  
-   **代理历史记录清除：分发**  
  
-   **分发的复制监视刷新器。**  
  
-   **复制代理检查**  
  
-   **分发清除：分发**  
  
-   **过期订阅清除**  
  
 从  的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from the **Agents** tab in Replication Monitor. 有关启动复制监视器的信息，请参阅[启动复制监视器](../monitor/start-the-replication-monitor.md)。 在“作业属性 - \<作业>”对话框中查看和修改每个作业的属性，可从同一文件夹和选项卡中访问此对话框。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>在 Management Studio 中启动或停止复制维护作业  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击一个作业，然后单击 **“启动作业”** 或 **“停止作业”**。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>在复制监视器中启动或停止复制维护作业  
  
1.  在复制监视器中，展开发布服务器组，然后选择一个发布服务器。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  在网格中右键单击一个作业，然后单击 **“启动作业”** 或 **“停止作业”**。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>在 Management Studio 中查看和修改复制维护作业的属性  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击一个作业，然后单击 **“属性”**。  
  
4.  在“作业属性 - \<作业>”对话框中，根据需要修改任意属性，然后单击“确定”。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>在复制监视器中查看和修改复制维护作业的属性  
  
1.  在复制监视器中，展开发布服务器组，然后选择一个发布服务器。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  在网格中右键单击一个作业，然后单击 **“属性”**。  
  
4.  在“作业属性 - \<作业>”对话框中，根据需要修改任意属性，然后单击“确定”。  
  
## <a name="see-also"></a>请参阅  
 [启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [查看发布服务器的信息和执行其任务（复制监视器）](../monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [复制代理管理](../agents/replication-agent-administration.md)  
  
  