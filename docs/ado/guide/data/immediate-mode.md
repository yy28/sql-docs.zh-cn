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
author: rothja
ms.author: jroth
ms.openlocfilehash: d036b2fa33c2f9fd5696eeb2984d07d4217eff6e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757903"
---
# <a name="immediate-mode"></a>即时模式
当**LockType**属性设置为**adLockOptimistic**或**adLockPessimistic**时，即时模式有效。 在 "即时" 模式下，只要通过调用**Update**方法在行上声明工作完成，就会将对记录的更改传播到数据源。  
  
## <a name="calling-update"></a>调用更新  
 如果在调用**update**方法之前从要添加或编辑的记录中移动，ADO 将自动调用**update**以保存更改。 如果要取消对当前记录所做的任何更改或放弃新添加的记录，则必须在导航前调用**CancelUpdate**方法。  
  
 在调用**Update**方法之后，当前记录保持为最新。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用**CancelUpdate**方法可以取消对当前行所做的任何更改，或者放弃新添加的行。 在调用**Update**方法之后，不能取消对当前行或新行所做的更改，除非这些更改是可使用**RollbackTrans**方法或批更新的一部分回滚的事务的一部分。 对于批更新，可以使用**CancelUpdate**或**CancelBatch**方法取消**更新**。  
  
 如果在调用**CancelUpdate**方法时添加新行，则当前行将成为在**AddNew**调用之前的当前行。  
  
 如果尚未更改当前行或添加了新行，则调用**CancelUpdate**方法将生成错误。
