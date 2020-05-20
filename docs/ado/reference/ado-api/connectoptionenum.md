---
title: ConnectOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: rothja
ms.author: jroth
ms.openlocfilehash: fa372f05a80290e907298a0969d9eb9f14355f90
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762598"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法应在建立连接后返回（同步）还是在之前返回（异步）。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以异步方式打开连接。 可以使用[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件来确定连接何时可用。|  
|**adConnectUnspecified**|-1|默认。 同步打开连接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>应用于  
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)
