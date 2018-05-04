---
title: ExecuteComplete 事件 (ADO) |Microsoft 文档
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
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5de9c41a11d735c5f63796760d596582e6da1b1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 事件 (ADO)
**ExecuteComplete**命令执行完毕后，将调用事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 A**长**值，该值指示该命令影响的记录数。  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值**adStatus**是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用此事件时，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 此事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pCommand*  
 [命令](../../../ado/reference/ado-api/command-object-ado.md)已执行的对象。 包含**命令**对象调用的情况下，即使**Connection.Execute**或**Recordset.Open**而无需显式创建**命令**在哪些情况下**命令**ado 内部创建对象。  
  
 *pRecordset*  
 A[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)是在执行命令的结果的对象。 这**记录集**可能为空。 你应永远不会销毁记录集对象在此事件处理程序内。 这样将导致访问冲突，当 ADO 尝试访问不再存在的对象。  
  
 *pConnection*  
 A[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 连接对其执行该操作。  
  
## <a name="remarks"></a>注释  
 **ExecuteComplete**事件可能会发生由于**连接。**[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)，**命令。**[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)，**记录集。**[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)，**记录集。**[Requery](../../../ado/reference/ado-api/requery-method.md)，或**记录集。**[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)方法。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
