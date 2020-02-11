---
title: WillConnect 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: 9fc1ac74e7e3d521bae587957f5f95771e5a5268
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945850"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
在连接开始之前调用**WillConnect**事件。  
  
 **适用于：** [CONNECTION 对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>parameters  
 *ConnectionString*  
 一个**字符串**，其中包含挂起连接的连接信息。  
  
 *Id*  
 包含挂起连接的用户名的**字符串**。  
  
 *权限*  
 一个**字符串**，其中包含挂起的连接的密码。  
  
 *选项*  
 一个**长整型**值，该值指示提供程序应如何计算*ConnectionString*。 唯一的选择是**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 调用此事件时，默认情况下，此参数设置为**adStatusOK** 。 如果事件无法请求取消挂起操作，则将其设置为**adStatusCantDeny** 。  
  
 在此事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续通知。 将此参数设置为**adStatusCancel**可请求导致取消此通知的连接操作。  
  
 *pConnection*  
 此事件通知适用的[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 **WillConnect**事件处理程序对**连接**参数的更改将不会对**连接**产生任何影响。  
  
## <a name="remarks"></a>备注  
 调用**WillConnect**时， *ConnectionString*、 *UserID*、 *Password*和*Options*参数将设置为由导致此事件（挂起连接）的操作所建立的值，并且可以在事件返回之前进行更改。 **WillConnect**可能会返回挂起的连接被取消的请求。  
  
 当取消此事件时，将调用**ConnectComplete** ，并将其*adStatus*参数设置为**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
