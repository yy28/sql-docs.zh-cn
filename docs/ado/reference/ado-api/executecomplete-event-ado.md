---
title: ExecuteComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec656a49963eb02cb204d5be96d403726bba8c56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657725"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 事件 (ADO)
**ExecuteComplete**命令执行完毕后，将调用事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 一个**长**值，该值指示受命令影响的记录数。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了如果发生的错误的值**adStatus**是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用此事件时，此参数设置为**adStatusOK**引发该事件的操作是否成功，或向**adStatusErrorsOccurred**如果操作失败。  
  
 此事件返回之前，请将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pCommand*  
 [命令](../../../ado/reference/ado-api/command-object-ado.md)已执行的对象。 包含**命令**对象调用时甚至**Connection.Execute**或**Recordset.Open**而无需显式创建**命令**在哪些情况下**命令**通过 ADO 在内部创建对象。  
  
 *pRecordset*  
 一个[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，它执行的命令的结果。 这**记录集**可能为空。 您应永远不会销毁来自此事件处理程序中的此记录集对象。 ADO 尝试访问的对象不再存在时，执行此操作将导致访问冲突。  
  
 *pConnection*  
 一个[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 对其执行该操作的连接。  
  
## <a name="remarks"></a>备注  
 **ExecuteComplete**事件可能是由于**连接。**[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)，**命令。**[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)，**记录集。**[开放](../../../ado/reference/ado-api/open-method-ado-recordset.md)，**记录集。**[Requery](../../../ado/reference/ado-api/requery-method.md)，或**记录集。**[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
