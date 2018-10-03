---
title: 启动和停止复制代理 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 27760ba8e445660e1215bf2e23b922b1a783b553
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100169"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>启动和停止复制代理 (SQL Server Management Studio)
  可以从  中的 **“作业”** 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from “作业” Monitor. 可启动和停止以下代理和作业：  
  
-   快照代理，用于所有发布。  
  
-   日志读取器代理，用于所有事务发布。  
  
-   队列读取器代理，用于为排队更新订阅启用的事务发布。  
  
-   分发代理，用于同步对事务发布和快照发布的订阅。  
  
-   合并代理，用于同步对合并发布的订阅。  
  
-   复制维护作业。  
  
 有关启动合并代理和分发代理的详细信息，请参阅[同步推送订阅](../synchronize-a-push-subscription.md)和[同步请求订阅](../synchronize-a-pull-subscription.md)。 有关维护作业的详细信息，请参阅[运行复制维护作业 (SQL Server Management Studio)](../../../ssms/sql-server-management-studio-ssms.md)。  
  
 有关启动复制监视器的信息，请参阅[启动复制监视器](../monitor/start-the-replication-monitor.md)。  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>从 Management Studio 启动和停止快照代理或日志读取器代理  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点和 **“复制”** 文件夹。  
  
2.  展开 **“本地发布”** 文件夹，然后右键单击发布。  
  
3.  单击 **“查看快照代理状态”** 或 **“查看日志读取器代理状态”**。  
  
4.  单击 **“启动”** 或 **“停止”**。  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>从 Management Studio 启动和停止队列读取器代理  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击代理的作业，再单击 **“启动作业”** 或 **“停止作业”**。 队列读取器代理的作业名称的格式为 **[\<分发服务器>].\<整数>**。  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>从复制监视器启动和停止快照代理、日志读取器代理或队列读取器代理  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  右键单击代理，再单击 **“启动代理”** 或 **“停止代理”**。  
  
## <a name="see-also"></a>请参阅  
 [监视复制](../monitoring-replication.md)   
 [复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](replication-agents-overview.md)  
  
  
