---
title: “事务”事件类别 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0322fd84cf708b8310b7ec6e1483ae24d998617e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166958"
---
# <a name="transactions-event-category"></a>Transactions 事件类别
  **Transactions** 事件类可用于监视事务的状态。 带有 **TM:** 前缀的事件类名称可用于跟踪通过事务管理界面发送的、与事务相关的操作。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[DTCTransaction 事件类](dtctransaction-event-class.md)|跟踪由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 协调的事务。 这些是在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的两个或两个以上的数据库或实例之间分布的事务。|  
|[SQLTransaction 事件类](sqltransaction-event-class.md)|跟踪 [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN、COMMIT TRAN、SAVE TRAN 和 ROLLBACK TRAN 语句。|  
|[TM: Begin Tran Completed 事件类](tm-begin-tran-completed-event-class.md)|指明已完成 BEGIN TRANSACTION 请求。|  
|[TM: Begin Tran Starting 事件类](tm-begin-tran-starting-event-class.md)|指明正在启动 BEGIN TRANSACTION 请求。|  
|[TM: Commit Tran Completed 事件类](tm-commit-tran-completed-event-class.md)|指明已完成 COMMIT TRANSACTION 请求。|  
|[TM: Commit Tran Starting 事件类](tm-commit-tran-starting-event-class.md)|指明正在启动 COMMIT TRANSACTION 请求。|  
|[TM: Promote Tran Completed 事件类](tm-promote-tran-completed-event-class.md)|指明已完成 PROMOTE TRANSACTION 请求。|  
|[TM: Promote Tran Starting 事件类](tm-promote-tran-starting-event-class.md)|指明正在启动 PROMOTE TRANSACTION 请求。|  
|[TM: Rollback Tran Completed 事件类](tm-rollback-tran-completed-event-class.md)|指明已完成 ROLLBACK TRANSACTION 请求。|  
|[TM: Rollback Tran Starting 事件类](tm-rollback-tran-starting-event-class.md)|指明正在启动 ROLLBACK TRANSACTION 请求。|  
|[TM: Save Tran Completed 事件类](tm-save-tran-completed-event-class.md)|指明已完成 SAVE TRANSACTION 请求。|  
|[TM: Save Tran Starting 事件类](tm-save-tran-starting-event-class.md)|指明正在启动 SAVE TRANSACTION 请求。|  
|[TransactionLog 事件类](transactionlog-event-class.md)|跟踪事务何时写入数据库事务日志。|  
  
  
