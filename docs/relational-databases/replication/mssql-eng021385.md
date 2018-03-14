---
title: MSSQL_ENG021385 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c99c72b377f10999f55ad48a23e2b522308d0a2a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng021385"></a>MSSQL_ENG021385
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21385|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|快照无法处理发布 '%s'。 可能是由于活动架构的更改操作或者是所添加的新项目所致。|  
  
## <a name="explanation"></a>解释  
 如果快照代理开始运行时正在对发布数据库进行更改（包括添加或删除项目以及对已发布的对象执行架构更改），就会产生此错误。  
  
## <a name="user-action"></a>用户操作  
 完成对发布数据库的更改后，重新启动快照代理。 有关详细信息，请参阅[启动和停止复制代理 (SQL Server Management Studio)](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和[复制代理可执行文件概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
