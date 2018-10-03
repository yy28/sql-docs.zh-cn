---
title: MSSQL_ENG014150 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78a147080f33cb78b4a752d362d6f62c6123cdf9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674355"
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14150|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|复制 - %s：代理 %s 成功。 %s|  
  
## <a name="explanation"></a>解释  
 此消息指出复制代理已成功完成运行。 复制使用下列代理：  
  
-   快照代理。 该代理由所有发布使用。  
  
-   日志读取器代理。 该代理由所有事务发布使用。  
  
-   队列读取器代理。 该代理由为排队更新订阅启用的事务发布使用。  
  
-   分发代理。 该代理将订阅同步到事务发布和快照发布。  
  
-   合并代理。 该代理将订阅同步到合并发布。  
  
-   复制维护作业。  
  
## <a name="user-action"></a>用户操作  
 日志读取器代理、队列读取器代理和分发代理通常连续运行，而其他代理通常则按需要或按计划运行。 如果认为某个代理无法完成运行，请检查该代理的状态。 有关详细信息，请参阅 [Monitor Replication Agents](../../relational-databases/replication/monitor/monitor-replication-agents.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [复制分发代理](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [复制日志读取器代理](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [复制合并代理](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [复制队列读取器代理](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
