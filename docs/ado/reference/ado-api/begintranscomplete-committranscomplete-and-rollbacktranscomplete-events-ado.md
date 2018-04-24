---
title: BeginTrans，CommitTrans，如果不事件 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 05a5809043ca348d78c1d73cb362c8b2f99efc7c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)
这些事件将在关联的操作之后调用上[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象完成执行。  
  
-   **BeginTransComplete**后，会调用[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **CommitTransComplete**后，会调用[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **RollbackTransComplete**后，会调用[不](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *TransactionLevel*  
 A**长**值，该值包含新的事务级别**BeginTrans**导致此事件。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述 EventStatusEnum 的值是否发生的错误**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用了任何这些事件时，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 这些事件可以通过将此参数设置为阻止后续通知**adStatusUnwantedEvent**事件返回之前。  
  
 *pConnection*  
 **连接**对象发生此事件。  
  
## <a name="remarks"></a>注释  
 Visual c + + 中多个**连接**可以共享相同的事件处理方法。 该方法使用返回**连接**对象确定哪些对象引发事件的原因。  
  
 如果[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性设置为**adXactCommitRetaining**或**adXactAbortRetaining**，一个新的事务启动后提交或回滚事务。 使用**BeginTransComplete**事件，若要忽略所有但第一个事务开始事件。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、 CommitTrans，以及如果不方法示例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
