---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01325e8d83a5a7d7b65398f4e0cb981b1fca7540
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208919"
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1222|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LK_TIMEOUT|  
|消息正文|已超过了锁请求超时时段。|  
  
## <a name="explanation"></a>解释  
 另一个事务持有必需资源的锁的时间比此查询可以等待该资源的时间长。  
  
## <a name="user-action"></a>用户操作  
 执行以下任务以缓解该问题：  
  
1.  如有可能，请找出持有必需资源的锁的事务。 使用 **sys.dm_os_waiting_tasks** 和 **sys.dm_tran_locks** 动态管理视图。  
  
2.  如果事务仍持有该锁，请终止该事务（如何适合）。  
  
3.  重新执行查询。  
  
 如果频繁出现此错误，请更改锁超时期限，或者修改有问题的事务以便它们持有锁的时间减少。  
  
  
