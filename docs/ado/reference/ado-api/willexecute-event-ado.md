---
title: "WillExecute 事件 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords: WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5988a43be066f61019223eb6a501d1bc73e8bc23
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
**WillExecute**事件在连接上执行挂起命令之前调用。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 A**字符串**，其中包含的 SQL 命令或存储的过程名称。  
  
 *游标类型*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)包含类型的光标**记录集**将打开。 使用此参数，可以将光标更改为任何类型期间**记录集**[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)操作。 *游标类型*针对任何其他操作将被忽略。  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) ，其中包含的锁类型**记录集**将打开。 使用此参数，可以将锁更改为任何类型期间**RecordsetOpen**操作。 *LockType*针对任何其他操作将被忽略。  
  
 *选项*  
 A**长**值，该值指示用于执行命令或打开的选项**记录集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)可能的状态值**adStatusCantDeny**或**adStatusOK**当调用此事件。 如果它是**adStatusCantDeny**，此事件可能不会请求取消挂起操作。  
  
 *pCommand*  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)对象应用此事件通知。  
  
 *pRecordset*  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)对象应用此事件通知。  
  
 *pConnection*  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)对象应用此事件通知。  
  
## <a name="remarks"></a>注释  
 A **WillExecute**由于连接可能发生的事件。  [执行方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)，[执行方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)，或[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*pConnection*参数应始终包含对的有效引用**连接**对象。 如果事件的原因为**Connection.Execute**、 *pRecordset*和*pCommand*参数设置为**执行任何操作**。 如果事件的原因为**Recordset.Open**、 *pRecordset*参数将引用**记录集**对象和*pCommand*参数设置为**执行任何操作**。 如果事件的原因为**Command.Execute**、 *pCommand*参数将引用**命令**对象和*pRecordset*参数设置为**执行任何操作**。  
  
 **WillExecute**允许你检查和修改挂起的执行参数。 此事件可能会返回挂起命令被取消的请求。  
  
> [!NOTE]
>  如果原始源**命令**是由指定的流[CommandStream 属性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)属性，分配到一个新字符串**WillExecute** *源*参数将更改的源**命令**。 **CommandStream**会清除属性和[CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)属性将更新与新的源。 通过指定的原始流**CommandStream**将会发布并且无法访问。  
  
 如果新的源字符串内的方言组不同的原始设置[方言属性](../../../ado/reference/ado-api/dialect-property.md)属性 (这对应于**CommandStream**)，必须通过将设置指定的正确方言**方言**属性所引用的命令对象*pCommand*。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
