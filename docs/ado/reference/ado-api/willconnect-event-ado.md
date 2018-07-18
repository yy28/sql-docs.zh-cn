---
title: WillConnect 事件 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a2ddca516e9c5141e0e874074660579e8144ba7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282866"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
**WillConnect**连接开始之前，将调用事件。  
  
 **适用于：** [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 A**字符串**包含挂起的连接的连接信息。  
  
 *用户 Id*  
 A**字符串**包含挂起的连接的用户名。  
  
 *密码*  
 A**字符串**包含密码的挂起的连接。  
  
 *选项*  
 A**长**值，该值指示提供程序应如何评估*ConnectionString*。 唯一的选项是**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当调用此事件时，此参数设置为**adStatusOK**默认情况下。 设置为**adStatusCantDeny**如果事件不能请求取消挂起操作。  
  
 此事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。 将此参数设置为**adStatusCancel**请求引起此通知的取消的连接操作。  
  
 *pConnection*  
 [连接](../../../ado/reference/ado-api/connection-object-ado.md)对象应用此事件通知。 更改为的参数**连接**通过**WillConnect**事件处理程序不会有影响**连接**。  
  
## <a name="remarks"></a>Remarks  
 当**WillConnect**调用时， *ConnectionString*， *UserID*，*密码*，和*选项*参数设置为建立导致此事件 （挂起的连接），并可以更改事件返回之前的操作的值。 **WillConnect**可能会返回取消挂起的连接的请求。  
  
 取消此事件时， **ConnectComplete**将随调用其*adStatus*参数设置为**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
