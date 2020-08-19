---
description: ConnectComplete 和 Disconnect 事件 (ADO)
title: " (ADO) 的 ConnectComplete 和断开连接事件 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: db04bbeed12f9097768763024270ece7275d5c3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444539"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 和 Disconnect 事件 (ADO)
连接启动后，调用 **ConnectComplete** 事件。 连接结束后，将调用 " **断开** 连接" 事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>参数  
 *pError*  
 一个 [错误](../../../ado/reference/ado-api/error-object.md) 对象。 它描述了 *adStatus* 的值为 **adStatusErrorsOccurred**时所发生的错误;否则，不会设置。  
  
 *adStatus*  
 始终返回**adStatusOK**的[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)值。  
  
 调用**ConnectComplete**时，如果**WillConnect**事件已请求取消挂起的连接，此参数将设置为**adStatusCancel** 。  
  
 在任一事件返回之前，将此参数设置为 **adStatusUnwantedEvent** 以防止后续通知。 但是，关闭并重新打开 [连接](../../../ado/reference/ado-api/connection-object-ado.md) 会导致这些事件再次出现。  
  
 *pConnection*  
 应用此事件的 **连接** 对象。  
  
## <a name="see-also"></a>另请参阅  
 [ (VC + + 的 ADO 事件模型示例) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
