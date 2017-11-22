---
title: "类型的锁 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9a0f58e602b919d8dc5a048743809e1e4786414
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="types-of-locks"></a>类型的锁
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 指示开放式批量更新。 批处理更新模式，所需。  
  
 许多应用程序在一次提取的行数，然后需要进行包括整个要插入、 更新或删除的行集的协调的更新。 使用批处理游标，只有一个需要舍入到服务器的行程，因而可提高更新性能并降低网络流量。 使用批处理光标库，可以创建静态游标，然后断开与数据源连接。 此时你可以对行进行更改并随后重新连接并将更改发布到批处理中的数据源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指示提供程序使用乐观锁定-仅在调用锁定记录**更新**方法。 是否有另一个用户可以更改的时间之间的数据可能这意味着你编辑记录，当调用**更新**，这将创建冲突。 在其中发生冲突的可能性较低的情况下使用此锁类型或冲突可以轻松地解决。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 指示悲观锁定，记录的记录。 提供程序执行必要的操作以确保成功编辑的记录，通常通过锁定记录在紧靠之前编辑数据源。 当然，这意味着一旦开始编辑，通过调用释放锁之前，将不能供其他用户记录**更新。** 在系统中不能承受进行并发更改数据，如在订票系统中使用此类型的锁定。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 指示只读的记录。 无法更改的数据。 只读锁是锁定"快"类型，因为它不需要服务器维护的记录的锁。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 未指定锁的类型。
