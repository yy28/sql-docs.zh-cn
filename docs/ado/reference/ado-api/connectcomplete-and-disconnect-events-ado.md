---
title: ConnectComplete 和 Disconnect 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1466b8f718318d8224ec2c7dcf3e873139fffed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309158"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 和 Disconnect 事件 (ADO)
**ConnectComplete**连接启动后，将调用事件。 **断开连接**连接结束后，将调用事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了如果发生的错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)值，它始终返回**adStatusOK**。  
  
 当**ConnectComplete**是调用，此参数设置为**adStatusCancel**如果**WillConnect**事件已请求取消挂起的连接。  
  
 这两个事件返回之前，此参数设置为**adStatusUnwantedEvent**以防止后续的通知。 但是，关闭并重新打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)导致这些事件再次发生。  
  
 *pConnection*  
 **连接**对象应用此事件。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
