---
description: ConnectOptionEnum
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
ms.openlocfilehash: 71142aac94003987267a6d4a6b30d2c9d17c1bfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444419"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定在 (同步建立连接后，是否应返回[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法) 或 (异步) 之前返回。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以异步方式打开连接。 可以使用 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) 事件来确定连接何时可用。|  
|**adConnectUnspecified**|-1|默认。 同步打开连接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>适用于  
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)
