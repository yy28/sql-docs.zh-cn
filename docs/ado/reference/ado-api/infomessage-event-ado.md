---
title: InfoMessage 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edc451ae2075a22c106f4e2395836e7d508a7808
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694784"
---
# <a name="infomessage-event-ado"></a>InfoMessage 事件 (ADO)
**InfoMessage**只要期间出现警告时调用事件**ConnectionEvent**操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 此参数包含返回的任何错误。 如果返回了多个错误，枚举**错误**集合以找到它们。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 如果出现警告时， *adStatus*设置为**adStatusOK**并*pError*包含警告。  
  
 此事件返回之前，请将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pConnection*  
 一个[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 连接出现警告。 例如，可能出现警告，当打开**连接**对象或执行[命令](../../../ado/reference/ado-api/command-object-ado.md)上**连接**。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
