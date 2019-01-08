---
title: '&lt;AgentProfileName&gt; 属性 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.profiles.perfprofileprops.f1
helpviewer_keywords:
- Agent Profile Properties dialog box
ms.assetid: 01a992d2-e4ff-417c-93f0-dc43ab2d1624
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2ecd6ec8584eb4031e7d2c8a0af95204a930498
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763569"
---
# <a name="ltagentprofilenamegt-properties"></a>&lt;AgentProfileName&gt; 属性
  可以使用 **“代理配置文件属性”** 对话框查看为配置文件中的每个代理参数指定的值，以及修改用户定义的配置文件的值。  
  
## <a name="options"></a>选项  
 **名称**  
 配置文件的名称。  
  
 **说明**  
 关于配置文件的说明。  
  
 **参数**  
 配置文件中包含的代理参数。 配置文件无需指定每个参数值。 若要查看对给定代理有效的所有参数，请清除 **“仅显示此配置文件中使用的参数”** 复选框。 有关每个参数的说明，请参阅：  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [复制日志读取器代理](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [复制合并代理](agents/replication-merge-agent.md)  
  
-   [复制队列读取器代理](agents/replication-queue-reader-agent.md)  
  
 **默认值**  
 每个代理参数的默认值。  
  
 **值**  
 配置文件中指定的参数值。 对于用户定义的配置文件，此字段是可编辑的。  
  
 **“仅显示此配置文件中使用的参数”**  
 清除此复选框将会显示给定代理的所有有效参数。  
  
## <a name="see-also"></a>请参阅  
 [使用复制代理配置文件](agents/work-with-replication-agent-profiles.md)   
 [复制代理概述](agents/replication-agents-overview.md)   
 [复制代理配置文件](agents/replication-agent-profiles.md)  
  
  
