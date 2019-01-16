---
title: WillExecute 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 234a0eeba57958063a6f2eedb8510486df8a53a0
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255500"
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
**WillExecute**连接上执行的挂起命令之前调用事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 一个**字符串**，其中包含 SQL 命令或存储的过程名称。  
  
 *CursorType*  
 一个[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)包含类型的光标**记录集**将打开。 使用此参数，可以将光标更改为任何类型期间**记录集**[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)操作。 *CursorType*将被忽略的任何其他操作。  
  
 *LockType*  
 一个[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) ，其中包含的锁类型**记录集**将打开。 使用此参数，可以将锁更改为任何类型期间**RecordsetOpen**操作。 *LockType*将被忽略的任何其他操作。  
  
 *选项*  
 一个**长**值，该值指示可用于执行命令或打开的选项**记录集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)可能的状态值**adStatusCantDeny**或**adStatusOK**时调用此事件。 如果它是**adStatusCantDeny**，此事件可能不会请求取消的挂起的操作。  
  
 *pCommand*  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)应用此事件通知对象。  
  
 *pRecordset*  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)应用此事件通知对象。  
  
 *pConnection*  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)应用此事件通知对象。  
  
## <a name="remarks"></a>备注  
 一个**WillExecute**事件可能是由于连接。  [Execute 方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)， [Execute 方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)，或[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*pConnection*参数应始终包含对的有效引用**连接**对象。 如果事件是由于**Connection.Execute**，则*pRecordset*并*pCommand*参数设置为**Nothing**。 如果事件是由于**Recordset.Open**，则*pRecordset*参数将引用**记录集**对象和*pCommand*参数设置为**Nothing**。 如果事件是由于**Command.Execute**，则*pCommand*参数将引用**命令**对象和*pRecordset*参数设置为**Nothing**。  
  
 **WillExecute** ，可检查和修改挂起的执行参数。 此事件可能会返回挂起的命令被取消的请求。  
  
> [!NOTE]
>  如果原始的源**命令**是一个由指定的流[CommandStream 属性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)属性，分配到一个新字符串**WillExecute** _源_参数将更改的源**命令**。 **CommandStream**属性将被清除并且[CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)属性将更新与新的源。 指定的原始流**CommandStream**将发布的无法访问。  
  
 如果从的原始设置不同的新的源字符串的方言[Dialect 属性](../../../ado/reference/ado-api/dialect-property.md)属性 (这对应于**CommandStream**)，必须通过设置指定正确的方言**方言**属性所引用的命令对象*pCommand*。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
