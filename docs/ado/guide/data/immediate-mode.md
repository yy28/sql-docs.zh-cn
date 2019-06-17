---
title: 即时模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37ad4cbc60ad4c08b65ff7f0db9b5c70245a96e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700591"
---
# <a name="immediate-mode"></a>即时模式
即时模式，则当**LockType**属性设置为**adLockOptimistic**或**adLockPessimistic**。 在直接模式下，对记录的更改传播到数据源通过调用声明的行的操作完成时，就立即**更新**方法。  
  
## <a name="calling-update"></a>调用更新  
 如果将从该记录移正在添加或编辑，然后再调**更新**方法，将自动调用 ADO**更新**以保存所做的更改。 必须调用**CancelUpdate**之前如果想要取消对当前记录所做的任何更改或放弃新添加的记录的导航方法。  
  
 当前记录保持最新调用后**更新**方法。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用**CancelUpdate**方法取消对当前行所做的任何更改或丢弃新添加的行。 调用后，无法取消对当前行或新行的更改**更新**方法，除非所做的更改，可以使用回滚的事务的一部分，否则**RollbackTrans**方法或部分在批处理更新。 在批处理更新的情况下，你可以取消**更新**与**CancelUpdate**或**CancelBatch**方法。  
  
 如果在调用时，你要添加新行**CancelUpdate**方法，将成为当前行的行之前的当前**AddNew**调用。  
  
 如果未更改的当前行或添加新行，则调用**CancelUpdate**方法将生成错误。
