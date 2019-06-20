---
title: WillConnect 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 01b5c20668f97c80ae5abdcbb213914c012c7359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710057"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
**WillConnect**连接开始之前，将调用事件。  
  
 **适用于：**[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 一个**字符串**，它包含挂起的连接的连接信息。  
  
 *UserID*  
 一个**字符串**包含挂起的连接的用户名。  
  
 *密码*  
 一个**字符串**包含密码的挂起的连接。  
  
 *选项*  
 一个**长**值，该值指示提供程序应该如何评估*ConnectionString*。 唯一的选项是**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当调用此事件时，此参数设置为**adStatusOK**默认情况下。 设置为**adStatusCantDeny**如果事件不能请求取消的挂起的操作。  
  
 此事件返回之前，请将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。 将此参数设置为**adStatusCancel**请求导致取消此通知的连接操作。  
  
 *pConnection*  
 [连接](../../../ado/reference/ado-api/connection-object-ado.md)应用此事件通知对象。 将更改为的参数**连接**通过**WillConnect**事件处理程序会产生任何影响**连接**。  
  
## <a name="remarks"></a>备注  
 当**WillConnect**调用时， *ConnectionString*， *UserID*，*密码*，并*选项*参数设置为建立由操作导致此事件 （挂起的连接），并可以进行更改之前该事件返回的值。 **WillConnect**可能会返回请求取消挂起的连接。  
  
 取消此事件时， **ConnectComplete**调用时将使用其*adStatus*参数设置为**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
