---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fae14de91b626fdb349f712f0311ccbe97929560
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315637"
---
# <a name="mssqleng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20557|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|代理关闭。 有关详细信息，请参阅作业 '%s' 的 SQL Server 代理作业历史记录。|  
  
## <a name="explanation"></a>解释  
 复制代理在没有将原因写入相应的历史记录表的情况下关闭，或代理在某个过程中关闭。  
  
## <a name="user-action"></a>用户操作  
  
-   重新启动代理，以查看此代理现在是否能正常运行。 有关详细信息，请参阅[启动和停止复制代理 (SQL Server Management Studio)](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和[复制代理可执行文件概念](concepts/replication-agent-executables-concepts.md)。  
  
-   查看代理历史记录和作业历史记录，寻找同时发生的其他错误。 有关如何在复制监视器中查看代理状态和错误详细资料的信息，请参阅以下主题：  
  
    -   有关快照代理、日志读取器代理和队列读取器代理，请参阅[查看与发布关联的代理的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
    -   有关分发代理和合并代理，请参阅[如何查看与订阅关联的代理的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
-   验证代理所访问的各计算机之间的基本连接是否正常，然后用实用工具（如 **sqlcmd** ）连接到每台计算机。 连接时，请使用代理建立连接使用的同一帐户。 有关每个代理帐户所需权限的详细信息，请参阅 [Replication Agent Security Model](security/replication-agent-security-model.md)。  
  
-   如果在创建或应用快照发生错误，请检查快照目录中的文件以查找错误。  
  
-   如果错误继续出现，请增加代理的日志记录并指定日志的输出文件。 根据错误的上下文，这可能提供导致该错误和其他错误消息的步骤。 有关如何配置复制日志记录的详细信息，请参阅 Microsoft 知识库文章 [312292](http://support.microsoft.com/kb/312292)。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
