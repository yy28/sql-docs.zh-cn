---
title: "即时模式 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b667a5ebb190ddd7c3507bc04e5f2fbcd25dca19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="immediate-mode"></a>即时模式
即时模式，则当**LockType**属性设置为**adLockOptimistic**或**adLockPessimistic**。 在即时模式下，对记录的更改会传播到数据源通过调用声明行上的操作完成时，就会立即**更新**方法。  
  
## <a name="calling-update"></a>调用更新  
 如果你将从该记录移正在添加或编辑，然后再调**更新**方法时，将自动调用 ADO**更新**以保存所做的更改。 必须调用**正在执行**之前导航，如果你想要取消对当前记录所做的任何更改或丢弃新添加的记录的方法。  
  
 当前记录后，仍当前调用**更新**方法。  
  
## <a name="cancelupdate"></a>正在执行  
 使用**正在执行**方法可取消对当前行进行任何更改，或放弃新添加的行。 您无法取消对当前行或新行的更改后调用**更新**方法，除非所做的更改是你可以回滚，事务的任一一部分**不**方法或部分批量更新。 对于批处理更新时，你可以取消**更新**与**正在执行**或**执行**方法。  
  
 如果在调用时，要添加新行**正在执行**方法，当前行变成之前的当前行**AddNew**调用。  
  
 如果你没有更改当前行或添加新行，则调用**正在执行**方法将生成错误。
