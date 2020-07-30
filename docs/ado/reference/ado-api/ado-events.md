---
title: ADO 事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: rothja
ms.author: jroth
ms.openlocfilehash: a93353be1737b38e7acb557a682e84cbb947c2a1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242867"
---
# <a name="ado-events"></a>ADO 事件

|事件|描述|  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**BeginTrans**操作后调用。|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**CommitTrans**操作后调用。|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在连接开始后调用。|  
|[断开连接](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在连接结束后调用。|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|尝试移到超过**记录集**末尾的行时调用。|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|执行完命令后调用。|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|在将较长异步操作中的所有记录都检索到**记录集**后调用。|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|在长时间异步操作期间定期调用，以报告当前已检索到**记录集中**的行数。|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在一个或多个**字段**对象的值更改后调用。|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|在**ConnectionEvent**操作期间出现警告时调用。|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在**记录集中**的当前位置发生更改后调用。|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在一个或多个记录发生更改后调用。|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在**记录集**更改后调用。|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**RollbackTrans**操作后调用。|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在挂起操作之前调用，更改**记录集中**一个或多个**字段**对象的值。|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在**记录集**的一个或多个记录（行）更改之前调用。|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在挂起的操作更改**记录集**之前调用。|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|在连接启动之前调用。|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|在此连接上执行挂起命令之前调用，并为用户给出检查和修改挂起执行参数的机会。|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在挂起的操作更改**记录集中**的当前位置*之前*，调用**WillMove**事件。|  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 B： ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
