---
title: 查看和修改复制代理命令提示符参数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce887109d154f2d0940507d06950bf918ff2ab4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957222"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>查看和修改复制代理命令提示符参数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  复制代理是接受命令行参数的可执行文件。 默认情况下，代理在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业步骤下运行，因此，可以使用“作业属性 - \<作业>”对话框来查看和修改这些参数。 此对话框可通过 **的** “作业” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 文件夹和复制监视器中的 **“代理”** 选项卡打开。 有关启动复制监视器的信息，请参阅[启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
> [!NOTE]  
>  对代理参数所做的更改在下次启动代理时生效。 如果代理连续运行，则必须停止该代理，然后重新启动。  
  
 虽然可以直接修改这些参数，但通常的做法还是通过代理配置文件来修改它们。 有关详细信息，请参阅 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 如果从 **“作业”** 文件夹访问代理作业，则请使用下表来确定代理作业名称和每个代理可用的参数。  
  
|代理|作业名称|有关参数列表，请参阅|  
|-----------|--------------|------------------------------------|  
|快照代理|**\<发布服务器>-\<发布数据库>-\<发布>-\<整数>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|合并发布分区的快照代理|**Dyn_\<发布服务器>-\<发布数据库>-\<发布>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|日志读取器代理|**\<发布服务器>-\<发布数据库>-\<整数>**|[复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|请求订阅的合并代理|**\<发布服务器>-\<发布数据库>-\<发布>-\<订阅服务器>-\<订阅数据库>-\<整数>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|推送订阅的合并代理|**\<发布服务器>-\<发布数据库>-\<发布>-\<订阅服务器>-\<整数>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|推送订阅的分发代理|**\<发布服务器>-\<发布数据库>-\<发布>-\<订阅服务器>-\<整数>***|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|请求订阅的分发代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>***\*|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|非 SQL Server 订阅服务器的推送订阅的分发代理|**\<发布服务器>-\<发布数据库>-\<发布>-\<订阅服务器>-\<整数>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|队列读取器代理|**[\<分发服务器>].\<整数>**|[复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*对于 Oracle 发布的推送订阅，它是“\<发布服务器>-\<发布服务器>”而不是“\<发布服务器>-\<发布数据库>”  
  
 \*\* 对于 Oracle 发布的请求订阅，它是“\<发布服务器>-\<分发数据库>”而不是“\<发布服务器>-\<发布数据库>”  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>从 Management Studio 中查看和修改复制代理命令行参数  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到相应的计算机，然后展开服务器节点：  
  
    -   对于请求订阅的分发代理和合并代理，连接到订阅服务器。  
  
    -   对于所有其他代理，连接到分发服务器。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击一个作业，然后单击 **“属性”**。  
  
4.  在“作业属性 - \<作业>”对话框的“步骤”页上，选择步骤“运行代理”，然后单击“编辑”。  
  
5.  在 **“作业步骤属性 - 运行代理”** 对话框中，编辑 **“命令”** 字段。  
  
6.  在这两个对话框上单击 **“确定”** 。  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>从复制监视器中查看和修改分发代理和合并代理的命令行参数  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **“查看详细信息”**。  
  
4.  在“订阅 <SubscriptionName>”窗口中，单击“操作”，然后单击“\<AgentName> 作业属性”。  
  
5.  在“作业属性 - \<作业>”对话框的“步骤”页上，选择步骤“运行代理”，然后单击“编辑”。  
  
6.  在 **“作业步骤属性 - 运行代理”** 对话框中，编辑 **“命令”** 字段。  
  
7.  在这两个对话框上单击 **“确定”** 。  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>从复制监视器中查看和修改快照代理、日志读取器代理和队列读取器代理命令行参数  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  右键单击网格中的代理，然后单击 **“属性”**。  
  
4.  在“作业属性 - \<作业>”对话框的“步骤”页上，选择步骤“运行代理”，然后单击“编辑”。  
  
5.  在 **“作业步骤属性 - 运行代理”** 对话框中，编辑 **“命令”** 字段。  
  
6.  在这两个对话框上单击 **“确定”** 。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [复制代理可执行文件概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
