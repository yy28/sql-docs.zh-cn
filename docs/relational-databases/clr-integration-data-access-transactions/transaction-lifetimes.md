---
title: 事务生命周期 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86ac25a9f820bd64d9c15c8f43e97cccb6e1fb96
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="transaction-lifetimes"></a>事务生存期
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程中启动的事务与在托管代码中启动的事务之间存在一个重大区别：公共语言运行时 (CLR) 代码在进入或退出 CLR 调用时不能使事务状态取消均衡。 注意此区别的以下含义：  
  
-   必须提交或回滚在 CLR 框架内启动的事务，否则在退出该框架时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将产生错误。  
  
-   在 CLR 代码内不能提交或回滚外部事务。  
  
-   尝试提交不在同一过程中启动的事务将导致运行时错误。  
  
-   尝试回滚不在同一过程中启动的事务将导致挂起事务（防止执行任何其他带副作用的操作）。 事务将断开连接，直到 CLR 代码离开作用域。 请注意当您在过程内检测到错误并想确保终止整个事务时，这可能很有用。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
