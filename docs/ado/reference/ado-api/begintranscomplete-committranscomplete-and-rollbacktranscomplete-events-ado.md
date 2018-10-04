---
title: BeginTrans、 CommitTrans RollbackTrans 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afd8b9d4a45bdc98388f1133b3478a1cfbe51e4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773445"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)
将对关联的操作之后调用这些事件[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象完成执行。  
  
-   **BeginTransComplete**后，会调用[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **CommitTransComplete**后，会调用[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **RollbackTransComplete**后，会调用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *TransactionLevel*  
 一个**长**值，该值包含的新事务级别**BeginTrans**导致此事件。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述的错误的发生 EventStatusEnum 值是否**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用其中的任何事件时，此参数设置为**adStatusOK**引发该事件的操作是否成功，或向**adStatusErrorsOccurred**如果操作失败。  
  
 这些事件可以通过将此参数设置为阻止后续通知**adStatusUnwantedEvent**事件返回之前。  
  
 *pConnection*  
 **连接**发生此事件的对象。  
  
## <a name="remarks"></a>备注  
 在 Visual c + +，多个**连接**可以共享同一个事件处理方法。 该方法使用返回**连接**对象，以确定哪个对象引发事件的原因。  
  
 如果[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性设置为**adXactCommitRetaining**或**adXactAbortRetaining**，提交或回滚事务后启动新事务。 使用**BeginTransComplete**要忽略所有事件，但第一个事务开始事件。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法示例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
