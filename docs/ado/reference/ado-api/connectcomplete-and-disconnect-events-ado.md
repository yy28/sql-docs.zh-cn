---
title: ConnectComplete 并断开连接事件 (ADO) |Microsoft 文档
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
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 268f9bb86667b94437ea2745753a823b4fdb9dbe
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 和断开连接事件 (ADO) 连接
**ConnectComplete**连接启动后，将调用事件。 **断开连接**连接结束后，将调用事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)值始终返回**adStatusOK**。  
  
 当**ConnectComplete**是调用，此参数设置为**adStatusCancel**如果**WillConnect**事件已请求取消挂起的连接。  
  
 这两个事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。 但是，关闭并重新打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)导致会再次发生，这些事件。  
  
 *pConnection*  
 **连接**对象为此事件时应用。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
