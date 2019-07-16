---
title: Cancel 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db369b32737c0e2dae4603a4a5a6c26cdd3a7142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920230"
---
# <a name="cancel-method-ado"></a>Cancel 方法 (ADO)
取消挂起的异步方法调用的执行。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>备注  
 使用**取消**终止执行的异步方法调用的方法： 一种方法，即调用使用了**adAsyncConnect**， **adAsyncExecute**，或者**adAsyncFetch**选项。  
  
 下表显示了在使用时终止的任务**取消**上特定类型的对象的方法。  
  
|如果*对象*是|终止对此方法的最后一个异步调用|  
|----------------------|-------------------------------------------------------------|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[“连接”](../../../ado/reference/ado-api/connection-object-ado.md)|[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)或[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[记录](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)， [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)， [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)，或[打开](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[流](../../../ado/reference/ado-api/stream-object-ado.md)|[打开](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>请参阅  
 [Cancel 方法示例 (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Cancel 方法示例 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法示例 （VC + +）](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute 方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)
