---
title: 锁的类型 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b66b87b0c741bf943cc2558862a0e1853c386b5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510726"
---
# <a name="types-of-locks"></a>锁定类型
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 表示开放式批量更新。 所需的批更新模式。  
  
 许多应用程序在一次提取的行数，然后需要进行协调的更新，其中包括整个要插入、 更新或删除的行集。 使用批处理游标，只有一个需要舍入到服务器的行程，从而提高了更新性能和减少网络流量。 使用批处理游标库，可以创建静态游标，然后断开与数据源的连接。 此时您可以对行进行更改并随后重新连接并将更改发布到一批中的数据源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指示提供程序使用乐观锁定-仅在调用时锁定记录**更新**方法。 这意味着还有另一个用户可能会更改数据的时间之间有机会编辑记录到当您调用**更新**，这将创建冲突。 在其中发生冲突的可能性较低的情况下使用此锁类型或冲突可以轻松地解析。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 指示悲观锁定，记录的记录。 提供程序执行必要的以确保成功编辑的记录，通常通过在数据源编辑之前立即锁定记录。 当然，这意味着，一旦您开始编辑，通过调用释放锁之前，将无法向其他用户使用记录**更新。** 在系统中您不能承受进行并发更改数据，例如在订票系统中使用这种类型的锁。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 指示只读的记录。 不能更改的数据。 只读锁是锁定的"最快"类型，因为它不需要服务器来维持的记录的锁。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 不会指定锁的类型。
